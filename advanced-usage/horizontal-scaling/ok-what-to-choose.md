# 😑 Ok, what to choose?

In case you don't know how your architecture should be, consult the following table and pick your use case:

| Use case                                                 | Recommended Adapter / Other adapters | Recommended Rate-Limiting Driver |
| -------------------------------------------------------- | ------------------------------------ | -------------------------------- |
| Single node, one thread                                  | Local                                | Local                            |
| Single node, multiple threads (PM2)                      | Cluster                              | Cluster                          |
| Multi-node, one thread, same Private Network             | Cluster/Redis                        | Cluster/Redis                    |
| Multi-node, multiple threads (PM2), same Private Network | Cluster/Redis                        | Cluster/Redis                    |
| Multi-node, one thread, multi-network                    | Redis                                | Redis                            |
| Multi-node, multiple threads (PM2), multi-network        | Redis                                | Redis                            |

{% hint style="info" %}
It's highly recommended to go for single-thread choices in multi-node architectures and scale horizontally on the instance level instead of both instances and threads.
{% endhint %}
