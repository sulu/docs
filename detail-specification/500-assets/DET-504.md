##![Assets](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/assets.png)DET-504 Media Rest Object

###Media Rest Object JSON

``` json
{
    'id': 1,
    'locale': 'en-gb',
    'collection': 1,
    'version': 3,
    'versions': [
        1,
        2,
        3
    ],
    'title': 'Media Title',
    'description: 'Media Description',
    'size': 12412512,
    'contentLanguages': [
        'en-gb',
        'de-at'
    ],
    'publishLanguages': [
        'en-gb',
        'de-at'
    ],
    'tags': [
        {
            'id': 1,
            'name': 'Tag 1'
        },
        {
            'id': 2,
            'name': 'Tag 2'
        }
    ],
    'name': 'photo.jpeg',
    'url': '/original/filename.jpg',
    'formats': [
      '170x170': '/uploads/sulumedia/150x100/filename.jpg',
      '960x': 'http://www.cdn.com/media/filename.jpg'
    ],
    'changer': 'Firstname Lastname',
    'creator': 'Firstname Lastname',
    'changed': '2014-01-01 16:00:00',
    'created': '2014-01-01 16:00:00'
}
```

###Media Rest Object Media - Multiple Files Concept JSON

GET /api/media/1

``` json
{
    'id': 1,
    'type': 'image', 
    'files': [
        {
            'id': 1,
            'title': 'File 1',
            'previewUrl': '/uploads/media/150x100/filename.jpg',
            'contentLanguages': [
                'en-gb',
                'en-us'
            ],
            'publishLanguages': [
                'en-gb',
                'en-us'
            ]
        },
        {
            'id': 2,
            'title': 'File 3',
            'previewUrl': '/uploads/media/150x100/filename2.jpg',
            'contentLanguages': [
                'de-de',
                'de-at'
            ],
            'publishLanguages': [
                'de-de',
                'de-at'
            ]
        }
    ]
}
```

###Media Rest Object File - Multiple Files Concept JSON

GET /api/files/1

``` json
{
    'id': 1,
    'locale': 'en-gb',
    'collection': 1,
    'version': 3,
    'versions': [
        1,
        2,
        3
    ],
    'title': 'File 1',
    'description: 'Media Description',
    'size': 12412512,
    'contentLanguages': [
        'en-gb',
        'de-at'
    ],
    'publishLanguages': [
        'en-gb',
        'de-at'
    ],
    'tags': [
        {
            'id': 1,
            'name': 'Tag 1'
        },
        {
            'id': 2,
            'name': 'Tag 2'
        }
    ],
    'name': 'photo.jpeg',
    'url': '/original/filename.jpg',
    'formats': [
      '170x170': '/uploads/sulumedia/150x100/filename.jpg',
      '960x': 'http://www.cdn.com/media/filename.jpg'
    ],
    'changer': 'Firstname Lastname',
    'creator': 'Firstname Lastname',
    'changed': '2014-01-01 16:00:00',
    'created': '2014-01-01 16:00:00'
}
```
, 
    
