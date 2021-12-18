# ↔ Horizontal Scaling

soketi is optimized to work in multi-node or multi-process environments like Kubernetes or PM2. However, as you may expect, the main concern when scaling horizontally is how to make the nodes communicate between each other.

To be able to scale horizontally and efficiently enable node-to-node or process-to-process communication, soketi leverages a [Redis connection](../getting-started/redis-configuration.md).

You can configure soketi to run using Redis as a primary adapter for all typically local-persistent data using the `ADAPTER_DRIVER` environment variable:

```
$ ADAPTER_DRIVER=redis soketi start
```

{% hint style="info" %}
Keep in mind: adapters like Redis are used for horizontal scaling only. Configuring and running Redis when running soketi using the `local` adapter will have no effect.
{% endhint %}

### Environment Variables

| Name                   | Default | Possible values  | Description                                                                              |
| ---------------------- | ------- | ---------------- | ---------------------------------------------------------------------------------------- |
| `ADAPTER_DRIVER`       | `local` | `redis`, `local` | The adapter driver to use to store and retrieve each app and channel's persistent data. |
| `ADAPTER_REDIS_PREFIX` | `''`    | Any string       | The Redis adapter's Pub / Sub channels prefix.                                             |

