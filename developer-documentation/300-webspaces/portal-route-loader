# PortalRouteLoader
The `SuluWebsiteBundle` includes a new `RouteLoader`, which listens to the portal type from the routing configurations.
So if you write a routing file like the following, this RouteLoader will load the routes:

```yaml
some_route_name:
    resource: "@BundleName/Resource/config/routing.yml"
    type: portal
```

The special thing is, that the routes will be generated, so that they match all Portals. So if there is a portal with a URL like `sulu.io/de` (assuming that the language is already resolved), the RouteLoader will create a Route, so that the Route `sulu.io/de/defined/path/for/route` will also match.
