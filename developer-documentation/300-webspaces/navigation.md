# Navigation

DefaultController.php

```
class DefaultController extends WebsiteController
{
	...
    public function indexAction(StructureInterface $structure, $preview = false, $partial = false)
    {
        $response = $this->renderStructure(
            $structure,
            array(
                'navigation' => $this->getMainNavigation($structure, null, $preview)
            ),
            $preview,
            $partial
        );
        return $response;
    }
	...
}

```

master.html.twig:

```
{% if navigation is defined %}
	{% include 'ClientWebsiteBundle:Website:navigation.html.twig' %}
{% endif %}
```

navigation.html.twig:

```
<ul>
    {% for item in navigation %}
        <li>
            <a href="{{ item.url }}" title="{{ item.title }}">{{ item.content.title }}</a>
            {% if item.children|length > 0 %}
                {% include 'ClientWebsiteBundle:Website:navigation.html.twig' with {navigation: item.children} %}
            {% endif %}
        </li>
    {% endfor %}
</ul>
```

__API__

* title: title attribute
* url: url to this page
* content: content structure