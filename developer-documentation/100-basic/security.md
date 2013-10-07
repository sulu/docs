# Security Bundle
## Roles
* used [AuraJS](https://github.com/massiveart/sulu-docs/blob/master/detail-specification/000-foundation/DET-003-Frontend.md)
* standard bundle with rest service for roles
* matrix component for displaying permissions in form/main.js
 * listen to events for changing permissions and update object which will be transfered by save event afterwards

## Authentication
* Used standard [http://symfony.com/doc/current/book/security.html#how-security-works-authentication-and-authorization](symfony components)
* configureable in `app/config/security.yml`
 * `security.encoders` defines the encoding for the password of each entity

## Authorization
* Used symfony components
* Implemented Voter for our own Permissions
* Implemented own UserProvider (for avoiding lazy loading)
* Check permissions in a Controller

```php
$this->get('security.context')->isGranted(array(
    'context' => 'Your security context',
    'permission' => 'view|add|edit|delete|archive|live|security',
    'locale' => 'Your locale' //this one is optional
));
```
