# Queues

Queues can be used to defer some code from running in the current WebSocket server. This feature is useful for queuing Webhook's HTTP requests in a different process so that it won't interfere with the WebSockets server. The default queue driver is `sync` and it will run in the same process. Consider using other drivers in case the WebSocket is heavily used.

| Name | Default | Possible values | Description |
| :--- | :--- | :--- | :--- |
| `QUEUE_DRIVER` | `sync` | `sync` | The driver used for the queues. |



