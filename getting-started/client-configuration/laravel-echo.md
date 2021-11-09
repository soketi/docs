# Laravel Echo

Laravel Echo is backward-compatible with the PusherJS library, meaning that it resembles most of the example configuration in the previous section:

```javascript
import Echo from 'laravel-echo';

window.Pusher = require('pusher-js');

let echoServer = new Echo({
    broadcaster: 'pusher',
    key: process.env.MIX_PUSHER_APP_KEY,
    wsHost: process.env.MIX_PUSHER_HOST,
    wsPort: process.env.MIX_PUSHER_PORT,
    forceTLS: false,
    encrypted: true,
    disableStats: true,
    enabledTransports: ['ws', 'wss'],
});

echoServer.private(`orders.${orderId}`)
    .listen('OrderShipmentStatusUpdated', (e) => {
        console.log(e.order);
    });
```

The `MIX_*` variables are declared in your .env file:

```
PUSHER_APP_KEY=app-key
PUSHER_APP_ID=app-id
PUSHER_APP_SECRET=app-secret
PUSHER_HOST=127.0.0.1
PUSHER_PORT=6001

MIX_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
MIX_PUSHER_HOST="${PUSHER_HOST}"
MIX_PUSHER_PORT="${PUSHER_PORT}"
```
