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
/workspaces/[ID]/nodes?parent=123-123-123&depth=1
```

### Example response

Response for request on `workspace/1234/nodes?depth=1`.

```
{
    "_links" : {
        "self": "/workspace/1234/nodes/1",
        "children" : "/workspace/1234/nodes?parent=1&depth=1",
    },
    "_embedded": [
            {
                "title": "Page 123",
                "id": "123",
                "hasSub": true,
                "published":true,
                "linked": internal,
                "type": {
                    "name": "ghost",
                    "value: "us_en"
                },
                "_links" : {
                     "self" : "/workspace/1234/nodes/123",
                     "children" : "/workspace/1234/nodes?parent=123&depth=1"
                 },
                 "_embedded": []
            }
    ],
    "title": "Root",
    "id": "1",
    "hasSub": true, 
}
```

__type.name__ can have following values: ghost (should have a value), shadow, false

__linked__  can have the values internal, external, false 
