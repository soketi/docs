# 🕛 Queues

Queues can be used to defer code from running within the current WebSocket server. This feature is useful for queuing Webhook requests in a different process so that they won't interfere with the performance of the main WebSockets server. The default queue driver is `sync` and will run in the same process as the current server, essentially disabling queuing.

However, when queueing using Redis, soketi will queue the job details in Redis and the job will eventually be processed later by one of soketi's queue workers so that your main server response time does not suffer.

{% hint style="info" %}
To run queues with Redis, you need to configure a [Redis connection](https://github.com/soketi/docs/blob/0.x/advanced-usage/getting-started/redis-configuration.md).
{% endhint %}

### Environment Variables

| Name                  | Default | Possible values | Description                 |
| --------------------- | ------- | --------------- | --------------------------- |
| `SOKETI_QUEUE_DRIVER` | `sync`  | `sync`, `redis` | The driver used for queues. |
