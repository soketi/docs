# 🧠 Horizontal Scaling with Redis

Before reading about queuing webhook processing using Redis, you may wish to [read the documentation regarding horizontal scaling](../horizontal-scaling.md).

When combining queuing and horizontal scalability, it's highly recommended that you use a third-party driver like Redis. Redis helps ensure that once a webhook is triggered it will be completely processed because the message to send the webhook will remain in-memory within Redis. Therefore, even if the soketi server goes down, the webhook will still be sent.

Each webhook message is processed by a worker. In addition, each worker can spawn multiple queue listeners. In soketi's case, each worker represents one of the listed events within the [app webhooks documentation](../app-webhooks.md). This way, soketi ensures that webhooks are being processed quickly and efficiently. **This behavior may be subject to change in the future. For example, queues for each app might eventually be needed to ensure high-performance message processing in all situations.**

### Environment Variables

| Name                      | Default | Possible values | Description                                               |
| ------------------------- | ------- | --------------- | --------------------------------------------------------- |
| `QUEUE_REDIS_CONCURRENCY` | `1`     | Any integer     | The number of webhook messages that can be processed in parallel for each event. |

