
# Plan Representation

## Main Structures

#### 01 Node Structure
Node structure is like an abstract base class of all nodes, it contains only a type field to identify the real node structure.

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


### ttt
