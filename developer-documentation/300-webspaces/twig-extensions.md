# Twig-Extensions

## WebsiteBundle

### ContentPathTwigExtension

`sulu_content_path(url, [webspaceKey = current])`

Returns absolute URL

* Parameter
  * url (string): Url to get path
  * webspaceKey (string) - optional: If item is not in the same webspace as current content
* Returns: `string`

__Example__:

```twig
<ul class="nav nav-justified">
    {% for item in content.snippets[0].internalLinks %}
        <li>
            <a href="{{ sulu_content_path(item.url, item.webspaceKey) }}" title="{{ item.title }}">{{ item.title }}</a>
        </li>
    {% endfor %}
</ul>
```

`sulu_content_root_path()`

Returns url for root node

* Returns: `string`

### ContentTwigExtension

`sulu_content_load(uuid)`

Returns content array for given uuid.

* Parameter
  * uuid (string): The uuid of requested content
* Returns: `array`
  * uuid
  * changed / changer / created / creator
  * content
  * view

`sulu_content_load_parent(uuid)`

Returns content array for given uuid.

* Parameter
  * uuid (string): The uuid the child of requested content node
* Returns: `array`
  * uuid
  * changed / changer / created / creator
  * content
  * view

### NavigationTwigExtension

`sulu_navigation_root_flat([context = null], [depth = 1], [loadExcerpt = false])`

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

`sulu_navigation_root_tree([context = null], [depth = 1], [loadExcerpt = false])`

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
 
`sulu_navigation_flat(uuid, [context = null], [depth = 1], [loadExcerpt = false], [level = null])`

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
 
`sulu_navigation_tree(uuid, [context = null], [depth = 1], [loadExcerpt = false], [level = null])`

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

__Example__:

```twig
{% set nav = sulu_navigation_tree(uuid) %}
<ul class="nav nav-justified">
    {% for item in nav %}
        <li>
            <a href="{{ sulu_content_path(item.url) }}" title="{{ item.title }}">{{ item.title }}</a>
        </li>
    {% endfor %}
</ul>
```
 
`sulu_breadcrumb(uuid)`

Returns breadcrumb (BreadcrumbItemInterface[]) for given content node.

* uuid (string): The uuid of the current content.

__Example__:

```twig
{% set nav = sulu_breadcrumb(uuid) %}
<ul class="nav nav-justified">
    {% for item in nav %}
        <li>
            <a href="{{ sulu_content_path(item.url) }}" title="{{ item.title }}">{{ item.title }}</a>
        </li>
    {% endfor %}
</ul>
```

### SitemapTwigExtension

`sulu_sitemap([locale = current], [webspaceKey = current])`

Returns sitemap for given Webspace and Locale (or default is the current locale and webspace).

* locale (string) - optional: locale for determine sitemap
* webspaceKey (string) - optional: webspace for determine sitemap

`sulu_sitemap_url(url, [locale = current], [webspaceKey = current])`

Returns url for given Webspace and locale.

* url (string): The uuid of the current content
* locale (string) - optional: locale for determine url
* webspaceKey (string) - optional: webspace for determine url

## SnippetBundle

`snippet_load(uuid, [locale = current])`

Returns content array for given uuid.

* Parameter
  * uuid (string): The uuid of requested content
  * locale (string) - optional: Locale to load snippet
* Returns: `array`
  * uuid
  * changed / changer / created / creator
  * content
  * view

## ContactBundle

TODO
