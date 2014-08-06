#DET-004 Routing

## Component Diagram
![Routing Diagram](https://raw.github.com/sulu-cmf/docs/master/detail-specification/images/diagrams/Routing.png)

## RequestListener
The requested portal is detected by the `RequestListener`, which listens on Symfony's `Kernel.REQUEST`-Event. We set a very high priority on this task, because we need this information already in the routing process, which already includes a very high prioritized listener on this event. 

The `RequestListener` only calls the `analyze`-method of the `RequestAnalyzer`, which analyzes the given Request, calculates and loads some values, and saves them in some variables.  The `RequestAnalyzer` is a service, so that you can use these values (MatchType, Webspace, Portal, PortalUrl, Language, Country, Redirect) from every place. Besides webspace and portal the MatchType is the most important value saved by the `RequestAnalyzer`, which can have one of the following values.

| MatchType     | Description
| ------------- | -----------
| Full Match    | The given URL starts with the value given from the portal, including the language and segment
| Partial Match | The given URL starts with the general URL from the portal, which does noet include the language and segment (e.g. for the pattern `{localization}.sulu.io` it just matches `sulu.io`. The standard behaviour is to redirect to the default language and segment
| Redirect      | There is a redirect URL defined, which means the current Request ist just redirected to it

The description above includes the standard behaviour, if there is a standard symfony route defined, it is handled before our dynamic routes, which means the controller called then decides on the behaviour. However, the controller can still use the values from the `RequestAnalyzer`.

##Routing
![Routing Process Diagram](https://raw.github.com/sulu-cmf/docs/master/detail-specification/images/diagrams/RoutingProcess.png)
First of all there is a check, if the requested page has a still valid entry in the cache. If yes, just this page has to be returned in a response.

For the general routing process the `ChainRouter` of the Symfony CMF is used. Together with its dynamic router it allows us to use dynamic routes. For this there is the `PortalRouteProvider`, which first analyzes the request with the `RequestAnalyzer`. Then the `RequestAnalyzer` can be used further, so that the request analyzation has only to be done once.

Afterwards the `PortalRouteProvider` checks if the request should be redirected, and redirects to a route returning a `RedirectResponse`. Otherwise it will set the current theme and try to load the content with the given path from the `ContentMapper`. The `ContentMapper` returns the structure of the current page, which is used to render the website. It passes the data to the template, and fills a response with the correct CacheHandlers. If the `ContentMapper` can't find any content, it will create a HttpNotFoundException, which will be resolved using a custom twig ExceptionController.
