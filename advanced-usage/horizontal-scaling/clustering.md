# 🧠 Clustering

Beside scaling horizontally, that can be done by configuring the [Redis adapter](../horizontal-scaling.md), each running instance of soketi is able to communicate with other nodes that run in the same private network via the  IPC protocol in Node.js.

The clustering method provides the alternative of running the communication between nodes without having to deal with a third-party channel like Redis Pub/Sub. The protocol is, in fact, decentralized.

Clustering is enabled automatically for running servers, and this is used in various cases, like storing [rate-limiting buckets](../../rate-limiting-and-limits/broadcast-rate-limiting.md) or [scaling horizontally in the same private network](../horizontal-scaling.md#cluster-adapter).

### Environment Variables

| Name                     | Default   | Possible values | Description                                                                              |
| ------------------------ | --------- | --------------- | ---------------------------------------------------------------------------------------- |
| `CLUSTER_CHECK_INTERVAL` | `500`     | Any number      | The amount of time (in ms) between checks to see if new instances joined the network.    |
| `CLUSTER_HOST`           | `0.0.0.0` | Any string      | The hostname to bind to the network.                                                     |
| `CLUSTER_MASTER_TIMEOUT` | `2000`    | Any number      | The amount of time (in ms) between checks to see if the master instance is alive.        |
| `CLUSTER_NODE_TIMEOUT`   | `2000`    | Any number      | The amount of time (in ms) between checks to see if the instances are alive.             |
| `CLUSTER_PORT`           | `11002`   | Any number      | The port to communicate with other instances.                                            |

{% hint style="info" %}
Make sure to choose the same port and hostname if you want the nodes to communicate between each other properly. Deploying multi-tenant architectures should use different ports or hostnames.
{% endhint %}