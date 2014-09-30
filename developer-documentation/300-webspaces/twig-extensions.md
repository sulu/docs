# Twig-Extensions

## WebsiteBundle

### ContentPathTwigExtension

`content_path(url)`

Returns absolute URL

* Parameter
  * item (NavigationItem|StructureInterface|array): Item to generate URL
* Returns: `string`

`content_root_path()`

Returns url for root node

### NavigationTwigExtension

`navigation_root_flat([context = null], [depth = 1], [loadExcerpt = false])`

Returns navigation from root in a flat list data-structure.

* Parameter
 * context (string) - optional: context to filter navigation
 * depth (integer) - optional: depth to load (1 - childs, 2 - childs and child of childs, ...)
 * loadExcerpt (boolean) - optional: load data from excerpt tab
* Returns: `array`
 * uuid
 * title
 * url
 * template
 * changed / changer / created / creator
 * template
 * nodeType
 * path
 * excerpt.* (if load-excerpt is true)

`navigation_root_tree([context = null], [depth = 1], [loadExcerpt = false])`

Returns navigation from root in a tree data-structure (each item has `children`).

* Parameter
 * context (string) - optional: context to filter navigation
 * depth (integer) - optional: depth to load (1 - childs, 2 - childs and child of childs, ...)
 * loadExcerpt (boolean) - optional: load data from excerpt tab
* Returns: `array`
 * uuid
 * title
 * url
 * template
 * changed / changer / created / creator
 * template
 * nodeType
 * path
 * children
 * excerpt.* (if load-excerpt is true)
 
`navigation_flat(uuid, [context = null], [depth = 1], [loadExcerpt = false], [level = null])`

Returns navigation for content node (uuid) at given level (in breadcrumb) or (if level null) sub-navigation of page. In a Tree flat list data-structure.
 
* Parameter
 * uuid (string): The uuid of the current content
 * depth (integer) - optional: depth of generated navigation
 * loadExcerpt (boolean) - optional: load data from excerpt tab
 * level (integer) - optional: level in breadcrumb
* Returns: `array`
 * uuid
 * title
 * url
 * template
 * changed / changer / created / creator
 * template
 * nodeType
 * path
 * excerpt.* (if load-excerpt is true)
 
`navigation_tree(uuid, [context = null], [depth = 1], [loadExcerpt = false], [level = null])`

Returns navigation for content node (uuid) at given level (in breadcrumb) or (if level null) sub-navigation of page. In a Tree data-structure (each item has `children`).

* Parameter
 * uuid (string): The uuid of the current content
 * depth (integer) - optional: depth of generated navigation
 * loadExcerpt (boolean) - optional: load data from excerpt tab
 * level (integer) - optional: level in breadcrumb 
* Returns: `array`
 * uuid
 * title
 * url
 * template
 * changed / changer / created / creator
 * template
 * nodeType
 * path
 * children
 * excerpt.* (if load-excerpt is true)
 
`breadcrumb(uuid)`

Returns breadcrumb (BreadcrumbItemInterface[]) for given content node.

* uuid (string): The uuid of the current content.

__Example__:

```twig
{% set nav = navigation_tree(uuid) %}
<ul class="nav nav-justified">
    {% for item in nav %}
        <li>
            <a href="{{ content_path(item.url) }}" title="{{ item.title }}">{{ item.title }}</a>
        </li>
    {% endfor %}
</ul>
```

### SitemapTwigExtension

`sitemap([locale = current], [webspaceKey = current])`

Returns sitemap for given Webspace and Locale (or default is the current locale and webspace).

* locale (string) - optional: locale for determine sitemap
* webspaceKey (string) - optional: webspace for determine sitemap

`sitemap_url(url, [locale = current], [webspaceKey = current])`

Returns url for given Webspace and locale.

* url (string): The uuid of the current content
* locale (string) - optional: locale for determine url
* webspaceKey (string) - optional: webspace for determine url

## ContactBundle

TODO
