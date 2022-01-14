# 🗃 Private Network Configuration

### Private Network Scaling

The clustering method provides the alternative of running the communication between nodes without having to deal with a third-party channel like Redis Pub/Sub. The protocol is, in fact, decentralized.

```bash
ADAPTER_DRIVER=cluster soketi start
```

No matter how many soketi processes you open with the Cluster driver, you will have built-in scalability without additional servers. It's highly recommended to use the cluster adapter when you deploy soketi behind the same private network with PM2 to acquire multithreading.

The only downside to the cluster adapter is that you can only scale processes or instances which are within the same network. The protocol used is tied to a hostname which should be the same for all instances. This can be highly effective when deploying to Kubernetes clusters or behind the firewall, in the same network. To deploy in multi-mesh architectures, consider using [Redis Pub/Sub](redis-configuration.md).

{% hint style="info" %}
Keep in mind you should also set the [Rate Limiting driver](broken-reference) to `cluster` to ensure the rate limiting is even across all your workers.
{% endhint %}

### Environment Variables

| Name                     | Default   | Possible values | Description                                                                           |
| ------------------------ | --------- | --------------- | ------------------------------------------------------------------------------------- |
| `CLUSTER_CHECK_INTERVAL` | `500`     | Any number      | The amount of time (in ms) between checks to see if new instances joined the network. |
| `CLUSTER_HOST`           | `0.0.0.0` | Any string      | The hostname to bind to the network.                                                  |
| `CLUSTER_MASTER_TIMEOUT` | `2000`    | Any number      | The amount of time (in ms) between checks to see if the master instance is alive.     |
| `CLUSTER_NODE_TIMEOUT`   | `2000`    | Any number      | The amount of time (in ms) between checks to see if the instances are alive.          |
| `CLUSTER_PORT`           | `11002`   | Any number      | The port to communicate with other instances.                                         |

{% hint style="info" %}
Make sure to choose the same port and hostname if you want the nodes to communicate between each other properly. Deploying multi-tenant architectures should use different ports or hostnames.
{% endhint %}

### Built-in IPC

IPC is enabled automatically for running servers, and this is used in various cases, like storing [rate-limiting buckets](../../rate-limiting-and-limits/broadcast-rate-limiting.md) or [scaling horizontally in the same private network](../horizontal-scaling.md#cluster-adapter).

Beside scaling horizontally, that can be done by configuring the [Redis adapter](../horizontal-scaling.md), each running instance of soketi is able to communicate with other nodes that run in the same private network via the IPC protocol in Node.js.
