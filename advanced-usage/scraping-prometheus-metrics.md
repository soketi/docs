# 📈 Prometheus Metrics

soketi has a Prometheus exporter built-in with a list of metrics that can help you have a better overview of the cluster & connections.  All you need to do is enable the feature in soketi and set up your own Prometheus server and make it scrap the HTTP REST API of each node that soketi runs on.

soketi exposes **publicly** the WebSockets & HTTP REST API servers on port `6001`. Starting with version 0.17.0, the metrics are served on port `9601`, that is not exposed by default to the internet so that the sensitive metrics will not require the complexity of an authentication system, so you can also scrape the metrics from your private network, or from the same server instance the server runs on.

{% hint style="warning" %}
Keep in mind that when configuring your firewalls, you should let users access port `6001` from the internet, but not port `9601`.
{% endhint %}

### Enabling Metrics

You may use the the `METRICS_ENABLED` environment variable to enable the metrics server.

```bash
METRICS_ENABLED=1 soketi start
```

```bash
curl http://127.0.0.1:9601/metrics
```

This is just a trimmed output. The exposed metrics are for both soketi connections and apps, as well as the Node.js built-in Prometheus metrics regarding the running processes, memory and CPU usage that can be quite useful for autoscaling or monitoring the running instance.

```
# HELP soketi_6001_connected The number of currently connected sockets.
# TYPE soketi_6001_connected gauge

# HELP soketi_6001_new_connections_total Total amount of soketi connection requests.
# TYPE soketi_6001_new_connections_total counter

# HELP soketi_6001_new_disconnections_total Total amount of soketi disconnections.
# TYPE soketi_6001_new_disconnections_total counter

# HELP soketi_6001_socket_received_bytes Total amount of bytes that soketi received.
# TYPE soketi_6001_socket_received_bytes counter

...
```

### Environment Variables

| Name                        | Default      | Possible values | Description                                                                                                                      |
| --------------------------- | ------------ | --------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `METRICS_ENABLED`           | `false`      | `true`, `false` | Whether to enable the metrics or not. For Prometheus, enabling it will expose a `/metrics` endpoint.                             |
| `METRICS_SERVER_PORT`       | `9601`       | Any number      | Changing this will expose the server to a different port. For security, you may not want to whitelist it in the server firewall. |
| `METRICS_DRIVER`            | `prometheus` | `prometheus`    | The driver used to scrap the metrics. For now, only `prometheus` is available. Soon, Pushgateway will be available.              |
| `METRICS_PROMETHEUS_PREFIX` | `soketi_`    | Any string      | The prefix to add to the metrics in Prometheus to differentiate from other metrics in Prometheus.                                |

