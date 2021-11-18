# 🕛 Queues

Queues can be used to defer some code from running in the current WebSocket server. This feature is useful for queuing Webhook's requests in a different process so that it won't interfere with the WebSockets server. The default queue driver is `sync` and it will run in the same process as the current server.

When running queues with Redis, soketi will add the specific job details to run in Redis and it will eventually be later picked by one of the workers so that your current response time for your users won't suffer.

{% hint style="info" %}
To run queues with Redis, you need to configure the [Redis Database connector](../../databases/redis-configuration.md).
{% endhint %}

### Environment Variables

| Name           | Default | Possible values | Description                     |
| -------------- | ------- | --------------- | ------------------------------- |
| `QUEUE_DRIVER` | `sync`  | `sync`, `redis` | The driver used for the queues. |
