#Routing

##PortalListener
The requested portal is detected by the `PortalListener`, which listens on Symfony's `Kernel.REQUEST`-Event. We set a very high priority on this task, because we need this information already in the routing process, which already includes a very high prioritized listener on this event. 

The `PortalListener` only sets the current Portal on the `PortalManager`. For this it uses the `findByUrl`-Method of the `PortalManager`. This is quite a heavy task, because we have to look through all portals. After the current portal is set, we can get it with a single array access.
