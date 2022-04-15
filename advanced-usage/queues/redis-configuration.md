# 🧠 Redis

Before reading about queuing webhook processing using Redis, you may wish to [read the documentation regarding horizontal scaling](../horizontal-scaling/).

When combining queuing and horizontal scalability, it's highly recommended that you use a third-party driver like [Redis](https://github.com/soketi/docs/blob/0.x/advanced-usage/getting-started/redis-configuration.md). Redis helps ensure that once a webhook is triggered it will be completely processed because the message to send the webhook will remain in-memory within Redis. Therefore, even if the soketi server goes down, the webhook will still be sent.

Each webhook message is processed by a worker. In addition, each worker can spawn multiple queue listeners. In soketi's case, each worker represents one of the listed events within the [app webhooks documentation](../app-webhooks/). This way, soketi ensures that webhooks are being processed quickly and efficiently. **This behavior may be subject to change in the future. For example, queues for each app might eventually be needed to ensure high-performance message processing in all situations.**

{% hint style="info" %}
To decouple the queue processors from the active WS/HTTP server, consider [setting `MODE=worker`](../horizontal-scaling/running-modes.md#mode-worker) and run a separate fleet for your workers.
{% endhint %}

{% hint style="success" %}
In case you want to scale your queue workers with Prometheus, the best solution is to use **** [bull\_exporter](https://github.com/UpHabit/bull\_exporter)
{% endhint %}

{% hint style="warning" %}
Redis Cluster mode may be broken in some cases. [Read more about BullMQ Redis Cluster configurations](https://docs.bullmq.io/bull/patterns/redis-cluster).
{% endhint %}

### Environment Variables

| Name                              | Default | Possible values | Description                                                                                                                                                                       |
| --------------------------------- | ------- | --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `SOKETI_QUEUE_REDIS_CONCURRENCY`  | `1`     | Any integer     | The number of webhook messages that can be processed in parallel for each event.                                                                                                  |
| `SOKETI_QUEUE_REDIS_CLUSTER_MODE` | `false` | `false`, `true` | Whether the client should be initialized for Redis Cluster. [You have to specify the `DB_REDIS_CLUSTER_NODES` value.](../../getting-started/redis-configuration.md#redis-cluster) |
