# 🛑 Graceful Shutdowns & Real-time monitoring

If you run soketi standalone in a cluster at scale, you may run into capacity issues. For example, RAM usage might be near the limit supported by your server and even if you decide to horizontally scale the servers, new connections might still come to servers that are near their memory limit.

When deploying soketi using Kubernetes, running [Network Watcher 5.0+](../network-watcher/installation.md) inside the same pod will solve these issues by continuously monitoring the current pod using soketi's "usage endpoint" (so a Prometheus Server is not needed) and labeling the pods that reach a specified usage threshold.

soketi is also embedded with a graceful shutdown operator. This means that upon closing the server, it closes all the active connections and tells them to reconnect again. When using Network Watcher, this is done automatically within the assigned pods in Kubernetes at the service and pod level. More details can be found within the [Network Watcher documentation](../network-watcher/installation.md).
