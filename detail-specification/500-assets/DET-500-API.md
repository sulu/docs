Collection API:
===============

Type: RestController  
URL: /api/collections

### GET Params
|Name|Description|Parameter|Multiple|Example|
|---|---|---|---|---|
|parent|filter collection for parent|any id of an collection|false|/api/collection?parent=1|



Media API:
===========

Type: RestController  
URL: /api/media

### GET Params
|Name|Description|Parameter|Multiple|Example|
|---|---|---|---|---|
|ids|filter for specific ids|any id of a media|true|/api/media?ids=1,3,4|
|collection|filter for media from a collection|any id of an collection|false|/api/media?collection=1|
|types|filter for specific media type|document,image,video,audio|true|/api/media?types=image,video|
