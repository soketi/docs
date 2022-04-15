# Laravel Echo

Laravel Echo is compatible with the PusherJS library. Therefore, its configuration resembles the typical configuration of a PusherJS client such as the example configuration in the previous section of documentation:

```javascript
import Echo from 'laravel-echo';

window.Pusher = require('pusher-js');

let laravelEcho = new Echo({
    broadcaster: 'pusher',
    key: process.env.MIX_PUSHER_APP_KEY,
    wsHost: process.env.MIX_PUSHER_HOST,
    wsPort: process.env.MIX_PUSHER_PORT,
    wssPort: process.env.MIX_PUSHER_PORT,
    forceTLS: false,
    encrypted: true,
    disableStats: true,
    enabledTransports: ['ws', 'wss'],
});

laravelEcho.private(`orders.${orderId}`)
    .listen('OrderShipmentStatusUpdated', (e) => {
        console.log(e.order);
    });
```

{% hint style="danger" %}
Make sure that `enabledTransports` is set to `['ws', 'wss']`. If not set, in case of connection failure, the client will try other transports such as XHR polling, which soketi doesn't support.
{% endhint %}

The `MIX_*` environment variables are typically declared in your Laravel application's `.env` file:

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

{% hint style="info" %}
For SSL configuration, see the [Pusher SDK example for SSL](pusher-sdk.md#ssl-configuration).
{% endhint %}
