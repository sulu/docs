# Websocket Component

[Look for a basic model here ...](https://github.com/sulu-cmf/docs/blob/master/developer-documentation/models/uml/websocket-component.vpp)

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
  var socket = WebsocketManager.getClient('admin');
  
  // all messages (polling currently not implemented in fallback)
  socket.onMessage(function(handler, message) { ... });
  
  // messages for a specific handler (polling currently not implemented in fallback)
  socket.addHandler('sulu_content.preview.frontend', function(handler, message)
  
  // direct return from message handler
  socket.send('sulu_content.preview', {test: 'test'}).then(function(handler, message) { ... });
});
```

## Context

Each connection has a context for the whole session, it is identified by the session id, so it can be switched between websocket and fallback without reinitializing.

```php
// set a parameter
$context->set('test', 'test');

//get a parameter
$param = $context->get('test');
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
   $context = $this->getContext($from);
   ...
   $this->saveContext($context);
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
  
  // all messages (polling currently not implemented in fallback)
  socket.onMessage(function(handler, message) { ... });
  
  // messages for a specific handler (polling currently not implemented in fallback)
  socket.addHandler('NOT IN USE', function(handler, message)
  
  // direct return from message handler
  socket.send('NOT IN USE', {test: 'test'}).then(function(handler, message) { ... });
});
```

### MessageHandler for admin websocket

```php
class PreviewMessageHandler implements MessageHandlerInterface
{
  /**
  * {@inheritdoc}
  */
  public function handle(ConnectionInterface $conn, array $message, MessageHandlerContext $context)
  {
    return array('data' => strtoupper($message['data']);
  }
}
```

```xml
 <service id="test" class="%test.class%">
     <tag name="sulu.websocket.message.handler" dispatcher="admin" alias="test" />
 </service>
```

```javascript
define(['websocket-manager'], function(WebsocketManager) {
 var client = WebsocketManager.getClient('admin');
 this.client.send('test', { data: 'testdata' }).then(function(handler, message) { console.log('Result: ' + message.data); });
});
```

```
Result: TESTDATA
```
