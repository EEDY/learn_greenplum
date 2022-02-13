
# Plan Representation

## Main Structures

#### 01 Node Structure
Node structure is like an abstract base class of all nodes, it contains only one type field to identify the real node structure.
You can convert a Node struct to it's real struct type based on the type, eg. T_SelectStmt -> SelectStmt struct.

```
/*
 * The first field of a node of any type is guaranteed to be the NodeTag.
 * Hence the type of any node can be gotten by casting it to Node. Declaring
 * a variable to be of Node * (instead of void *) can also facilitate
 * debugging.
 */
typedef struct Node
{
	NodeTag		type;
} Node;
```

Type of all nodes are defined as enum NodeTag
```
/*
 * The first field of every node is NodeTag. Each node created (with makeNode)
 * will have one of the following tags as the value of its first field.
 *
 * Note that inserting or deleting node types changes the numbers of other
 * node types later in the list.  This is no problem during development, since
 * the node numbers are never stored on disk.  But don't do it in a released
 * branch, because that would represent an ABI break for extensions.
 */
typedef enum NodeTag
{
	T_Invalid = 0,

	/*
	 * TAGS FOR EXECUTOR NODES (execnodes.h)
	 */
	T_IndexInfo,
	T_ExprContext,
    ...

	/*
	 * TAGS FOR PLAN NODES (plannodes.h)
	 */
	T_Plan,
	T_Scan,
	T_Join,
    ...
    
	/*
	 * TAGS FOR STATEMENT NODES (mostly in parsenodes.h)
	 */
	T_RawStmt,
	T_Query,
	T_PlannedStmt,
	T_InsertStmt,
	T_DeleteStmt,
	T_UpdateStmt,
	T_SelectStmt,
```


#### 02 Sub Node Structs




## Representation of Trees

prepare a table with 100,000 rows
```
create table t100 ( a int, b int, c int ) ;
insert into t100 select generate_series(1, 100000), generate_series(100000, 200000), generate_series(200000, 300000);
```


```
select count(*) from t100;
```

#### 01 parser tree
the parser tree in postmaster of sql above is like:
```
"(
{RAWSTMT
  :stmt {
    SELECT
      :distinctClause <> 
      :intoClause <> 
      :targetList ({
        RESTARGET
          :name <> 
          :indirection <> 
          :val 
            {FUNCCALL
              :funcname (\"count\") 
              :args <> 
              :agg_order <> 
              :agg_filter <> 
              :agg_within_group false 
              :agg_star true 
              :agg_distinct false 
              :func_variadic false 
              :over <> 
              :location 7
            }
          :location 7
      }) 
      :fromClause ({
        RANGEVAR
          :catalogname <> 
          :schemaname <> 
          :relname t100 
          :inh true 
          :relpersistence p 
          :alias <> 
          :location 21
      })
      :whereClause <> 
      :groupClause <> 
      :havingClause <> 
      :windowClause <> 
      :valuesLists <> 
      :sortClause <> 
      :scatterClause <> 
      :limitOffset <> 
      :limitCount <> 
      :lockingClause <> 
      :withClause <> 
      :op 0 
      :all false 
      :larg <> 
      :rarg <> 
      :disableLockingOptimization false
  }
  :stmt_location 0 
  :stmt_len 26
}
)"
```


### ttt
