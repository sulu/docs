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


### Example URI

A request on the following uri will return the first level of nodes which means all direct childrend from the root node.

```
/workspaces/[ID]/nodes?depth=1
```

A request on the following uri will return the first level of nodes which means all direct childrend from the node with id 123-123-123.

```
/workspaces/[ID]/nodes?paretn=123-123-123&depth=1
```

### Example response
```
{
    "_links" : {
        "self": "/workspace/[ID]/nodes/1",
        "children" : "/workspace/[ID]/nodes?parent=1depth=1",
    },
    "_embedded": [
            {
                "title": "Page 123",
                "id": "123",
                "hasSub": true,
                "_links" : {
                     "self" : "/workspace/[ID]/nodes/123",
                     "children" : "/workspace/[ID]/nodes?parent=123depth=1"
                 },
                 "_embedded": []
            }
    ],
    "title": "Root",
    "id": "1",
    "hasSub": true, 
}
```
