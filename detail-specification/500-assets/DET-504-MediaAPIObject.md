##![Assets](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/assets.png)DET-504 Media Rest Object

###Media Rest Object JSON

``` json
{
    'id': 1,
    'locale': 'en-gb',
    'collection': 1,
    'version': 3,
    'versions': {
        1: {
            'version': 1,
            'url': '/media/1/download/media.jpg?v=1',
            'created': '1985-01-22 00:00'
        },
        2: {
            'version': 2,
            'url': '/media/1/download/media.jpg?v=2',
            'created': '1990-03-06 00:00'
        },
        3: {
            'version': 3,
            'url': '/media/1/download/media.jpg?v=3',
            'created': '1991-09-23 00:00'
        },
    },
    'title': 'Media Title',
    'description: 'Media Description',
    'size': 12412512,
    'downloadCounter': 1,
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
    'mimeType': 'image/jpeg',
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
    'downloadCounter': 1,
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
    'downloadCounter': 1,
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
    'mimeType': 'image/jpeg',
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

