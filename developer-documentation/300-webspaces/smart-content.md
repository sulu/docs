# Smart-Content configuration

Loaded data contains default following values:

* uuid
* title
* url
* urls
* nodeType
* changed / changer / created / creator
* nodeType
* path
* template

It is posible to configure loaded data over xml-template

```xml
<property name="pages" type="smart_content">
    ...

    <params>
        <param name="properties" type="collection">
            <param name="title" value="title"/>
            <param name="article" value="article"/>
            <param name="ext_title" value="excerpt.title"/>
            <param name="ext_tags" value="excerpt.tags"/>
            <param name="ext_images" value="excerpt.images"/>
        </param>
    </params>
</property>
```

__Remarks:__
* `title` - is a property of the structure
* `excerpt.title` - is a property of the `excerpt` structure extension withthe name `title`

__Usage:__
```html
{% for page in content.pages %}
    <div class="col-lg-4">
        <h2>
            <a href="{{ content_path(page.url) }}">{{ page.title }}</a>
        </h2>
        <p>
            <i>{{ page.ext_title }}</i> | <i>{{ page.ext_tags|join(', ') }}</i>
        </p>
        {% if page.ext_images|length > 0 %}
            <img src="{{ page.ext_images[0].thumbnails['50x50'] }}" alt="{{ page.ext_images[0].title }}"/>
        {% endif %}
        {% autoescape false %}
        {% if page.article != '' %}
            {{ page.article }}
        {% else %}
            <p>No Article found</p>
        {% endif %}
        {% endautoescape %}
    </div>
{% endfor %}
```

