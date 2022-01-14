# Pusher SDK

Pusher clients are fully compatible with the WebSocket protocol implemented by soketi, which means you can easily take advantage of amazing features like private channels, presence channels, and client events. You simply need to point the Pusher compatible client to the soketi server address:

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

When running the server in SSL mode, you may consider setting the `forceTLS` client option to `true`. When this option is set to `true`, the client will connect to the `wss` protocol instead of `ws`:

```javascript
const PusherJS = require('pusher-js');

let client = new PusherJS('app-key', {
    ...
    forceTLS: true,
    ...
});
```
