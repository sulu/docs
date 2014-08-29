# Twig-Extensions

## WebsiteBundle

### ContentPathTwigExtension
`content_path(item)`

Returns URL for given item

* item (NavigationItem|StructureInterface|array): Item to generate URL

`content_root_path()`

Returns url for root node

### NavigationTwigExtension

`navigation(uuid, webspaceKey, localization, depth, layer)`

Returns navigation for content node at given level (in breadcrumb) or (if level null) sub-navigation of page
 
* uuid (string): The uuid of the current content
* webspaceKey (string): The key for the current webspace
* localization (string): The localization code for the translation
* depth (integer): depth of generated navigation
* level (integer): level in breadcrumb 

`breadcrumb(uuid, webspaceKey, localization)`

Returns breadcrumb (BreadcrumbItemInterface[]) for given content node.

* uuid (string): The uuid of the current content
* webspaceKey (string): The key for the current webspace
* localization (string): The localization code for the translation

__BreadcrumbItemInterface__ contains:

* title
* uuid
* depth

__Example__:

```twig
{% set nav = navigation(uuid, webspaceKey, localization) %}
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
