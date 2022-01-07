# ↔ Horizontal Scaling

soketi is optimized to work in multi-node or multi-process environments like Kubernetes or PM2. However, as you may expect, the main concern when scaling horizontally is how to make the nodes communicate between each other. To be able to scale horizontally and efficiently enable node-to-node or process-to-process communication, soketi leverages a [Redis connection](../getting-started/redis-configuration.md).

You can configure soketi to run using Redis as a primary adapter for all typically local-persistent data using the `ADAPTER_DRIVER` environment variable:

```
$ ADAPTER_DRIVER=redis soketi start
```

{% hint style="info" %}
Adapters like Redis are used for horizontal scaling only. Configuring and running Redis when running soketi using the `local` adapter will have no effect.
{% endhint %}

### Environment Variables

| Name                                 | Default   | Possible values             | Description                                                                              |
| ------------------------------------ | --------- | --------------------------- | ---------------------------------------------------------------------------------------- |
| `ADAPTER_DRIVER`                     | `local`   | `redis`, `local`, `cluster` | The adapter driver to use to store and retrieve each app and channel's persistent data.  |
| `ADAPTER_REDIS_PREFIX`               | `''`      | Any string                  | The Redis adapter's Pub / Sub channels prefix.                                           |

### Cluster adapter

The cluster adapter is really useful when you want a decentralized, peer-to-peer method to communicate between nodes or processes. 

No matter how many soketi processes you open with the Cluster driver, you will have built-in scalability without additional servers. It's highly recommended to use the cluster adapter when you deploy soketi behind the same private network with PM2 to acquire multithreading.

The only downside to the cluster adapter is that you can only scale processes or instances which are within the same network. The protocol used is tied to a hostname which should be the same for all instances. This can be highly effective when deploying to Kubernetes clusters or behind the firewall, in the same network. To deploy in multi-mesh architectures, consider using Redis Pub/Sub.

{% hint style="info" %}
Make sure to choose the same port and hostname if you want the nodes to communicate between each other properly. Deploying multi-tenant architectures should use different ports or hostnames.
{% endhint %}

### Which drivers to choose?

In case you don't know how your architecture should be, consult the following table and pick your use case:

| Use case                                                 | Recommended Adapter / Other adapters          | Recommended Rate-Limiting Driver |
| -------------------------------------------------------- | --------------------------------------------- | -------------------------------- |
| Single node, one thread                                  | Local                                         | Local                            |
| Single node, multiple threads (PM2)                      | Cluster                                       | Cluster                          |
| Multi-node, one thread, same Private Network             | Cluster/Redis                                 | Cluster/Redis                    |
| Multi-node, multiple threads (PM2), same Private Network | Cluster/Redis                                 | Cluster/Redis                    |
| Multi-node, one thread, multi-network                    | Redis                                         | Redis                            |
| Multi-node, multiple threads (PM2), multi-network        | Redis                                         | Redis                            |

{% hint style="info" %}
It's highly recommended to go for single-thread choices in multi-node architectures and scale horizontally on the instance level instead of both instances and threads.
{% endhint %}