# 🧠 Horizontal Scaling with Redis

In case you are not familiar with methods and architecture on how to set pWS to be horizontal scaling ready, consider [reading the documentation about Horizontal Scaling](../horizontal-scaling.md).

For queuing, in case you decide to horizontally scale the server, it's highly recommended to use a third-party driver like Redis. Redis will ensure that once the webhook is triggered, it will surely be processed because the message to send the webhook will remain in-memory, and even if the server gets down, the webhook will be sent.

Each webhook message is being processed by a Worker. Each Worker can spawn multiple listeners, depending on the usage. In pWS's case, each worker represents one of the listed events in [App Webhooks](../app-webhooks.md). This way, pWS makes sure that webhooks are not being clogged by all of the events at once. **This is a subject of change in the future and perhaps queues for each app might be needed to ensure high-performance message processing.**

You may manually define the concurrency for each Worker, which means "how many messages can be processed at once for each message".

| Name | Default | Possible values | Description |
| :--- | :--- | :--- | :--- |
| `QUEUE_REDIS_CONCURRENCY` | `1` | Any integer | The number of parallel processed messages for each event. |



