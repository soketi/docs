# 🔀 New traffic redirection

Usually, on horizontal scalable models, you should now when to scale up or down. Mostly, in Soketi you should do it based on:

* memory - having low memory can be tough for new sockets as it's needed to store new user data on each new connection and actually having memory to store the pointer to the connection
* CPU - having low remaining CPU can increase the latency of your connections and mesages

For instances that run in [non-worker mode](../horizontal-scaling/running-modes.md#soketi\_mode-worker), you can check if they can receive new connections according to a threshold:

```bash
# If usage is < 75% of the allowed memory, the endpoint return 200 OK.
HTTP_ACCEPT_TRAFFIC_MEMORY_THRESHOLD=75 soketi start
```

This threshold can be tweaked by specifying the `HTTP_ACCEPT_TRAFFIC_MEMORY_THRESHOLD`, which is the percent of memory at which the `/accept-traffic` request will return a non-200 OK response. This way, you can configure your infrastructure in such a way that you can route the new traffic to instances that return 200 OK instead of pressuring a random algorithm that will not ensure best available memory instances first.

```bash
curl -X GET http://localhost:6001/accept-traffic
```

Alternatively, for Kubernetes there is [Network Watcher](broken-reference), which is a sidecar container that will automatically handle the pod labels to redirect traffic to pods that are having enough memory. Network Watcher is not influenced by this particular endpoint
