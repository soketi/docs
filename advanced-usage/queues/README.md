# 🕛 Queues

Queues can be used to defer some code from running in the current WebSocket server. This feature is useful for queuing Webhook's HTTP requests in a different process so that it won't interfere with the WebSockets server. The default queue driver is `sync` and it will run in the same process as the current server.

| Name           | Default | Possible values | Description                     |
| -------------- | ------- | --------------- | ------------------------------- |
| `QUEUE_DRIVER` | `sync`  | `sync`, `redis` | The driver used for the queues. |
