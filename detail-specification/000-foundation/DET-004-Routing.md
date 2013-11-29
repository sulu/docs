#DET-004 Routing

## Component Diagram
![Routing Diagram](https://raw.github.com/sulu-cmf/docs/master/detail-specification/images/diagrams/Routing.png)

## RequestListener
The requested portal is detected by the `RequestListener`, which listens on Symfony's `Kernel.REQUEST`-Event. We set a very high priority on this task, because we need this information already in the routing process, which already includes a very high prioritized listener on this event. 

The `RequestListener` only calls the `analyze`-method of the `RequestAnalyzer`, which analyzes the given Request, calculates and loads some values, and saves them in some variables.  The `RequestAnalyzer` is a service, so that you can use these values (Portal, PortalUrl, Language, Country, Redirect) from every place.

##Routing
![Routing Process Diagram](https://raw.github.com/sulu-cmf/docs/master/detail-specification/images/diagrams/RoutingProcess.png)
The general routing process is using the `ChainRouter` of the Symfony CMF. Together with its dynamic router it allows us to use dynamic routes. For this there is the `PortalRouteProvider`, which passes the URI of the current request to the `ContentMapper`. The `ContentMapper` returns the structure of the current page, which is used to render the website.

The `PortalRouteProvider` creates a new Route with the required information, and redirects to the `DefaultController`, respectively to the controller and view defined in the Template.

The default controller makes a lookup for the current URL in the `PortalManager`, and sets the according theme. The `LiipThemeBundle` will then resolve the paths to the Twig-templates in respect of the active theme.
