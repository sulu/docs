# Navigation

master.html.twig:

```html
{% include 'ClientWebsiteBundle:Website:navigation.html.twig' with {items:navigation_root_tree('main')}%}
```

navigation.html.twig:

```html
<ul>
    {% for item in items %}
        <li>
            <a href="{{ item.url }}" title="{{ item.title }}">{{ item.title }}</a>
            {% if item.children|length > 0 %}
                {% include 'ClientWebsiteBundle:Website:navigation.html.twig' with {items: item.children} %}
            {% endif %}
        </li>
    {% endfor %}
</ul>
```

__API__

* uuid
* title
* url
* urls
* nodeType
* changed / changer / created / creator
* nodeType
* path
* template
* children (optional)

