# HREF-Lang Tags

## Pages

Inspired by: https://support.google.com/webmasters/answer/189077?hl=de

__EXAMPLE (meta.html.twig):__
```html
{% for locale, url in urls if locale != request.locale%}
<link rel="alternate" href="{{ content_path((url?:'/'),request.webspaceKey,locale) }}" hreflang="{{ locale }}" />
{% endfor %}

<link rel="alternate" href="{{ content_path('/',request.webspaceKey,request.defaultLocale) }}" hreflang="x-default" />
```

## XML-Sitemap

Inspired by: https://support.google.com/webmasters/answer/2620865?hl=de

```xml
...
<url>
  <loc>{{ url }}</loc>
  <lastmod>{{ site.changed|date("Y-m-d") }}</lastmod>
{% for locale, url in site.urls if url is not null %}
  <xhtml:link rel="alternate" hreflang="{{ locale }}" href="{{ content_path(url, site.webspaceKey, locale) }}"/>
{% endfor %}
</url>
...
```
