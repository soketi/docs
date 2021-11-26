# 🎨 Client Configuration

Pusher clients are fully compatible with the WebSocket protocol implemented in this project. You just have to point the client to the server address:

```javascript
const PusherJS = require('pusher-js');

let client = new PusherJS('app-key', {
    wsHost: '127.0.0.1',
    wsPort: 6001,
    forceTLS: false,
    encrypted: true,
    disableStats: true,
    enabledTransports: ['ws', 'wss'],
});

client.subscribe('chat-room').bind('message', (message) => {
    alert(`${message.sender} says: ${message.content}`);
});
```

### SSL Configuration

When running the server in SSL mode, you might want to have `forceTLS` set to `true`. This way, the client will connect to the `wss` protocol instead of `ws`:

```javascript
const PusherJS = require('pusher-js');

let client = new PusherJS('app-key', {
    ...
    forceTLS: true,
    ...
});
```
