# Websocket Component

TODO diagram

The component was buil to add simple new websocket applications. It encapsules the routing of applications, running and create connections.

There are two parts of it:

* PHP Backend
  * AppManager
  * Commands
* JS-Frontend
  * Require component: which is able to connect to an app by name

## Backend

Composed of AppManager, Commands, BasicApp class.

### AppManaer

Used to add apps adnd run server. The standard implementation uses [Ratchet Websocket](http://socketo.me/docs/) library.

### Commands

```bash
$ app/console sf sulu:websocket:dump
+----------------------+------------------+-----------------+-----------+
| App-Name             | Route            | Allowed-Origins | Host-Name |
+----------------------+------------------+-----------------+-----------+
| sulu_content.preview | /content/preview | Array           | localhost |
|                      |                  | (               |           |
|                      |                  |     [0] => *    |           |
|                      |                  | )               |           |
|                      |                  |                 |           |
+----------------------+------------------+-----------------+-----------+
```

Dumps all registered apps with their routes and addtitional informations.

```bash
$ app/console sulu:websocket:run
Websocket server started: "ws://localhost:9876/<route>" bound to IP 127.0.0.1
```
Starts websocket server.

## Frontend

The frontend component creates connections for applications

```js
define(['websocket-manager'], function(WebsocketManager) {
  var socket = WebsocketManager.getClient('sulu_content.preview');
  
  socket.onopen = function() { ... };
  socket.onmessage = function() { ... };
  socket.onerror = function() { ... };
});
```

## Create App

### Normal Websocket:

```php
class TestMessageComponent extends AbstractWebsocketApp implements MessageComponentInterface
{
  protected $name = 'test';
    
 public function onOpen(ConnectionInterface $conn)
 {
   parent::onOpen($conn);
   ...
 }
 public function onMessage(ConnectionInterface $conn)
 {
   ...
 }
 public function onClose(ConnectionInterface $conn)
 {
   parent::onClose($conn);
   ...
 }
 public function onError(ConnectionInterface $conn, \Exception $e)
 {
   ...
 }
}
```

```xml
 <service id="websocket.component" class="TestMessageComponent">
     <tag name="sulu.websocket.app" route="/test" />
 </service>
```

```js
define(['websocket-manager'], function(WebsocketManager) {
  var socket = WebsocketManager.getClient('test');
  
  socket.onopen = function() { ... };
  socket.onmessage = function() { ... };
  socket.onerror = function() { ... };
});
```
