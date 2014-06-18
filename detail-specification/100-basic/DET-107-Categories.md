##![basic](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/basic.png)DET-107 Categories
#### REST-Api
``` json
{
    'id': 1,
    'locale': 'en',
    'name': 'My Category',
    'meta': [
        {
            'id': 1,
            'key': 'description',
            'value': 'This is a neat description of the category'
        },
        {
            'id': 2,
            'key': 'some-key',
            'value': 'Some value'
        },
    ],
    'creator': 'Firstname Lastname',
    'changer': 'Firstname Lastname',
    'created': '2014-01-01 16:00:00',
    'changed': '2014-01-01 16:00:00'
}
```
```
#### CGet - Parameters
The CGet-Action can be filtered with a "parent" parameter, which should contain the id of a parent
and a "depth" parameter which contains the level for which the categories should be output. (first level depth is 0)
