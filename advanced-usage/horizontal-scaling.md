# ↔ Horizontal Scaling

soketi is optimized to work in multi-node or multi-process environments, like Kubernetes or PM2, where horizontal scalability is one of the main core features that can be built upon. The main concern when scaling horizontally is **how can I make the nodes communicate between them?**

To be able to scale it horizontally and efficiently enable node-to-node or process-to-process communication, soketi leverages a Redis connection.

You can configure soketi to run with Redis as a primary adapter for the local-persistent data with an environment variable:

```
$ ADAPTER_DRIVER=redis soketi start
```

### Environment Variables

| Name                   | Default | Possible values  | Description                                                                              |
| ---------------------- | ------- | ---------------- | ---------------------------------------------------------------------------------------- |
| `ADAPTER_DRIVER`       | `local` | `redis`, `local` | The adapter driver to use to store and retrieve each app with channels' persistent data. |
| `ADAPTER_REDIS_PREFIX` | `''`    | Any string       | The Redis adapter's Pub/Sub channels prefix.                                             |

