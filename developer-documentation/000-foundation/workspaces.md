# Workspaces
Workspaces define the different content areas in Sulu. It should contain a key and a name, defines some localizations (combination of language and country), some optional segments of the website, and all its portals. The portals define a concrete portal, which means a website which contains the content from this website.
A portal only shows the content in the given localizations. The most important point is the url definition in the environment tag (have a look at [workspace detailspecification](https://github.com/sulu-cmf/docs/blob/master/detail-specification/300-webspaces/DET-302-workspaces.md) for more details).

## URL Definition
The most interesting part of this workspace definition are the URLs. An url should contain the language, country and (if existing) the segment which is used for this address. This can be done as attributes on the tag, or as placeholders, written in curly braces.

The following snippets show the two possibilities to define a url.

```xml
<url>{language}.sulu.{country}</url>
<url language="en" country="us">www.sulu.com</url>
```

If these values are not defined anywhere an exception will be thrown. This exception will be caught in the generation of the cache for the workspaces, so that this configuration file will be skipped and a warning will be written in the log.
In one case it is allowed to omit these values: if you have defined a redirect on the URL:

```xml
<url redirect="en.sulu.uk">www.sulu.uk</url>
```

That's because we don't need any of these values, since we redirect the request as soon as a redirect attribute is found.
