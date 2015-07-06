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
            'created': "2015-01-16T07:54:30+0100",
            'changed': "2015-01-16T07:54:30+0100"
        },
        2: {
            'version': 2,
            'url': '/media/1/download/media.jpg?v=2',
            'created': "2015-01-16T07:54:30+0100",
            'changed': "2015-01-16T07:54:30+0100"
        },
        3: {
            'version': 3,
            'url': '/media/1/download/media.jpg?v=3',
            'created': "2015-01-16T07:54:30+0100",
            'changed': "2015-01-16T07:54:30+0100"
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

