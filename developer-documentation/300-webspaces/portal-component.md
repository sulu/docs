# Portal Component
## Usage
```php
$portalManager = $container->get('sulu_core.portal.portal_manager');
$portal = $portalManager->findByKey('sulu_io');
```
This snippet returns the portal with the key sulu_io, and returns the portal object. There are also other methods to find a portal with different parameters.
