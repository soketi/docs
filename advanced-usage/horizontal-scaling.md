# ↔ Horizontal Scaling

pWS is optimized to work in multi-node or multi-process environments, like Kubernetes or PM2, where horizontal scalability is one of the main core features that can be built upon. The main concern when scaling horizontally is **how can I make the nodes communicate between them?**

To be able to scale it horizontally and efficiently enable node-to-node or process-to-process communication, pWS leverages a Redis connection.

You can configure pWS to run with Redis as a primary adapter for the local-persistent data with [an environment variable](../environment-variables/available-environment-variables/):

```text
$ ADAPTER_DRIVER=redis pws-server start
```



