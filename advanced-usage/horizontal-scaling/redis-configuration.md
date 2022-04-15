# 🧠 Redis Configuration

soketi is optimized to work in multi-node or multi-process environments like Kubernetes or PM2. However, as you may expect, the main concern when scaling horizontally is how to make the nodes communicate with each other. To be able to scale horizontally and efficiently enable node-to-node or process-to-process communication, soketi leverages a [Redis connection](../../getting-started/redis-configuration.md).

You can configure soketi to run using Redis as a primary adapter for all typically local-persistent data using the `ADAPTER_DRIVER` environment variable:

```
$ SOKETI_ADAPTER_DRIVER=redis soketi start
```

{% hint style="info" %}
Adapters like Redis are used for horizontal scaling only. Configuring and running Redis when running soketi using the `local` adapter will have no effect.
{% endhint %}

### Environment Variables

{% hint style="info" %}
These are the Redis variables to configure the adapter for Redis. For the rest of them, like host, port, and clustering support, read [Redis Configuration.](../../getting-started/redis-configuration.md#environment-variables)
{% endhint %}

| Name                                | Default | Possible values                     | Description                                                                                                                                                                       |
| ----------------------------------- | ------- | ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `SOKETI_ADAPTER_DRIVER`             | `local` | `redis`, `nats`, `local`, `cluster` | The adapter driver to use to store and retrieve each app and channel's persistent data.                                                                                           |
| `SOKETI_ADAPTER_REDIS_PREFIX`       | `''`    | Any string                          | The Redis adapter's Pub / Sub channels prefix.                                                                                                                                    |
| `SOKETI_ADAPTER_REDIS_CLUSTER_MODE` | `false` | `true`, `false`                     | Whether the client should be initialized for Redis Cluster. [You have to specify the `DB_REDIS_CLUSTER_NODES` value.](../../getting-started/redis-configuration.md#redis-cluster) |
