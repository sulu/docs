# Twig-Extensions

## WebsiteBundle

### ContentPathTwigExtension
`content_path(url)`

Returns absolute URL

* item (NavigationItem|StructureInterface|array): Item to generate URL

`content_root_path()`

Returns url for root node

### NavigationTwigExtension

`navigation_root_flat([context = null], [depth = 1], [loadExcerpt = false])`

Returns navigation from root

* context (string) - optional: context to filter navigation
* depth (integer) - optional: depth to load (1 - childs, 2 - childs and child of childs, ...)
* loadExcerpt (boolean) - optional ...



Returns navigation for content node at given level (in breadcrumb) or (if level null) sub-navigation of page
 
* uuid (string): The uuid of the current content
* webspaceKey (string): The key for the current webspace
* localization (string): The localization code for the translation
* depth (integer): depth of generated navigation
* level (integer): level in breadcrumb 

`breadcrumb(uuid, [webspaceKey], [localization])`

Returns breadcrumb (BreadcrumbItemInterface[]) for given content node.

* uuid (string): The uuid of the current content
* webspaceKey (string) - optional: The key for the current webspace
* localization (string) - optional: The localization code for the translation

__BreadcrumbItemInterface__ contains:

* title
* uuid
* depth

__Example__:

```twig
{% set nav = navigation_tree(uuid) %}
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
