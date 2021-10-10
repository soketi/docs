# ↔ Horizontal Scaling

pWS is optimized to work in multi-node or multi-process environments, like Kubernetes or PM2, where horizontal scalability is one of the main core features that can be built upon. The main concern when scaling horizontally is **how can I make the nodes communicate between them?**

To be able to scale it horizontally and efficiently enable node-to-node or process-to-process communication, pWS leverages a Redis connection.

You can configure pWS to run with Redis as a primary adapter for the local-persistent data with an environment variable:

```
$ ADAPTER_DRIVER=redis pws-server start
```

| Name                   | Default | Possible values  | Description                                                                              |
| ---------------------- | ------- | ---------------- | ---------------------------------------------------------------------------------------- |
| `ADAPTER_DRIVER`       | `local` | `redis`, `local` | The adapter driver to use to store and retrieve each app with channels' persistent data. |
| `ADAPTER_REDIS_PREFIX` | `''`    | Any string       | The Redis adapter's Pub/Sub channels prefix.                                             |

### Node Metadata

Node settings include assigning identifiers for the running node, this can be useful for horizontal scaling identity.

| Name      | Default              | Available values | Description                                                                                    |
| --------- | -------------------- | ---------------- | ---------------------------------------------------------------------------------------------- |
| `NODE_ID` | random UUIDv4 string | Any string       | A unique ID given to the node in which the process runs. Used by other features to label data. |
| `POD_ID`  | `null`               | Any string       | The Pod name if the app runs in Kubernetes. Used by other features to label data.              |

