# 😢 Known Limitations

### API

* The `/events` endpoint does not support passing channels via query strings
* The `/events` endpoint does not support the `info` parameter
* The `/batch_events` endpoint does not support the `info` parameter
* The `/channels` endpoint does not support `filter_by_prefix` and `info` parameters
* The `/channels/[channel_name`] endpoint does not support the `info`  parameter

### WebSockets

* Stats collection does not work
* The only transports for WebSockets are `ws` and `wss`

### Others

* Prometheus exists, but Datadog and Librato are not yet available ([See Pusher's note](https://pusher.com/docs/channels/miscellaneous/integrations/))
