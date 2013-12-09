# Nodes API

The api for nodes looks like in the following example:

```
/workspaces/[ID]/nodes
```

This example above will return all nodes available from the workspace with the [ID].

## Parameters

__parent__

With this parameter the starting point in the node tree can be set.

__depth__

With this parameter the depth can be limited which means from the start point x level of nodes will be returned.


### Example

A request on the following uri will return the first level of nodes which means all direct childrend from the root node.

```
/workspaces/[ID]/nodes?parent=null&depth=1
```

