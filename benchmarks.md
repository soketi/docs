# 🏆 Benchmarks

![](.gitbook/assets/medium\_90ms\_1536.png)

soketi is really fast!

In the scenario, there are 250 users that sit idle and receive 1 msg/s while 250 are actively connecting and disconnecting after 5 seconds.

The benchmark was done using an AWS `t3.small` instance (T3 Unlimited disabled to avoid bursting) @ 2 vCPU 2 GB and Gigabit network, in the `Europe Frankfurt` region. The ping between client location and server location was on average \~ 40ms.

The network overhead is taken into account by subtracting the ping twice, since the client trips once to the server to broadcast the message and trips one again back from the server to the client.

To calculate the internal time the server needs to process and distribute the received message, you can use the following formula:

```
INTERNAL_TIME = CALCULATED_DELAY - (NETWORK_PING * 2)
```

In this scenario, the processing time (excluding networking overhead) it takes for soketi to process a message in this scenario is:

```
INTERNAL_TIME = 119 - (40 * 2) = 119 - 80 = 39 ms
```

So for a  2 vCPU 2 GB instance, it takes the server `39ms` to distribute the messages for 250 concurrent users, in addition to a connecting-disconnecting ramp-up amount of between 100 and 250 users, and soketi really handles all of that.

### Performance Caveats

You may also want to consider additional overhead when deploying soketi:

* networking overhead, like in this benchmark or when horizontally scaling with Redis
* SSL/TLS overhead, that is caused by SSL natively
* the benchmarks didn't take into account the queues, if applicable, and these represent additional computing power needed to fulfill webhooks
* the benchmarks didn't take into account the HTTP requests for other non-broadcasting calls, since the benchmarks used only the HTTP API to publish 1 msg/s

When going to deploy in production for critical workload, consider the following:

#### Horizontally Scale soketi

soketi natively [scales horizontally with Redis Pub/Sub](advanced-usage/horizontal-scaling.md). This can add overhead for the internal Redis round-trips, but since you can horizontally scale, you are free to allocate resources dynamically.

By deploying soketi instances closer to Redis Read Replicas within a global Redis mesh, you can ensure low latency.

#### Deploy closer to your users

Most of the time, the biggest overhead is the latency itself. Consider deploying closer to your users for sub-100ms latency and develop a proper app mesh to ensure good horizontal scaling with Redis at the global scale.
