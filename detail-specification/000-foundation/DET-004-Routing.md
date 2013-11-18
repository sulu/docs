#DET-004 Routing

##Diagram
![Routing Diagram](https://raw.github.com/sulu-cmf/docs/master/detail-specification/images/diagrams/Routing.png)

##PortalListener
The requested portal is detected by the `PortalListener`, which listens on Symfony's `Kernel.REQUEST`-Event. We set a very high priority on this task, because we need this information already in the routing process, which already includes a very high prioritized listener on this event. 

The `PortalListener` only sets the current Portal on the `PortalManager`. For this it uses the `findByUrl`-Method of the `PortalManager`. This is quite a heavy task, because we have to look through all portals. After the current portal is set, we can get it with a single array access.

##Routing
The general routing process is using the `ChainRouter` of the Symfony CMF. Together with its dynamic router it allows us to use dynamic routes. For this there is the `PortalRouteProvider`, which passes the URI of the current request to the `ContentMapper`. The `ContentMapper` returns the structure of the current page, which is used to render the website.

The `PortalRouteProvider` creates a new Route with the required information, and redirects to the `DefaultController`, respectively to the controller and view defined in the Template.

The default controller makes a lookup for the current URL in the `PortalManager`, and sets the according theme. The `LiipThemeBundle` will then resolve the paths to the Twig-templates in respect of the active theme.
