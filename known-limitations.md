# 😢 Known Limitations

### API

* The `/events` endpoint does not support passing channels via query strings
* No endpoints support the `info` query parameter

### WebSockets

* Stats collection does not work
* The only transports for WebSockets are `ws` and `wss`

### Others

* Prometheus exists, but Datadog and Librato are not yet available ([See Pusher's note](https://pusher.com/docs/channels/miscellaneous/integrations/))
