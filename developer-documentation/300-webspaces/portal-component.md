# Workspace Component
## Usage
```php
$workspaceManager = $container->get('sulu_core.workspace.workspace_manager');
$workspace = $workspaceManager->findByKey('sulu_io');
```
This snippet returns the portal with the key sulu_io, and returns the portal object. There are also other methods to find a portal with different parameters.
