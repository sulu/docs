# Twig-Extensions

## WebsiteBundle

### ContentPathTwigExtension
`content_path(item)`

Returns URL for given item

* item (NavigationItem|StructureInterface|array): Item to generate URL

`content_root_path()`

Returns url for root node

### NavigationTwigExtension

`navigation(content, depth, layer)`

Returns navigation for content node at given level (in breadcrumb) or (if level null) sub-navigation of page
 
* content (StructureInterface): content node to generate navigation
* depth (integer): depth of generated navigation
* level (integer): level in breadcrumb 

`breadcrumb(content)`

Returns breadcrumb (BreadcrumbItemInterface[]) for given content node.

* content (StructureInterface): breadcrumb from root to this node (including)

__BreadcrumbItemInterface__ contains:

* title
* uuid
* depth

__Example__:

```twig
{% set nav = navigation(content) %}
<ul class="nav nav-justified">
    {% for item in nav %}
        <li>
            <a href="{{ content_path(item) }}" title="{{ item.title }}">{{ item.title }}</a>
        </li>
    {% endfor %}
</ul>

```

## ContactBundle

TODO
