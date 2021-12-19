# 📈 Prometheus Metrics

soketi has a Prometheus exporter built-in with a list of metrics that can help you have a better overview of the cluster and connections. To get started, enable the feature in soketi via the `METRICS_ENABLED` environment variable and set up your own Prometheus server to scrape the HTTP REST API of each node that soketi runs on.

soketi **publicly** exposes the WebSockets & HTTP REST API servers on port `6001`. Starting with version 0.17.0, soketi metrics are served on port `9601`, which is not publicly exposed to the Internet by default so that the sensitive metrics will not require the complexity of an authentication system. Therefore, you may easily scrape the metrics from your private network or from the same server instance the soketi server runs on.

{% hint style="warning" %}
When configuring your firewalls, keep in mind that you should let users access port `6001` from the Internet (so that messages can be broadcast), but not port `9601`.
{% endhint %}

### Enabling Metrics

You may use the the `METRICS_ENABLED` environment variable to enable the metrics server.

```bash
METRICS_ENABLED=1 soketi start
```

```bash
curl http://127.0.0.1:9601/metrics
```

A small sample of metrics output can be found below. The exposed metrics are for both soketi connections and apps, as well as the Node.js built-in Prometheus metrics regarding the running processes, memory, and CPU usage that can be useful for autoscaling or monitoring the running instance.

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

### Prometheus Metrics Environment Variables

| Name                        | Default      | Possible values | Description                                                                                                                      |
| --------------------------- | ------------ | --------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `METRICS_ENABLED`           | `false`      | `true`, `false` | Whether to enable metrics. For Prometheus, enabling this option will expose a `/metrics` endpoint.                             |
| `METRICS_SERVER_PORT`       | `9601`       | Any number      | The metrics server port. For security, this port should not be exposed to the Internet. |
| `METRICS_DRIVER`            | `prometheus` | `prometheus`    | The driver used to scrape metrics. For now, only `prometheus` is supported.
| `METRICS_PROMETHEUS_PREFIX` | `soketi_`    | Any string      | The prefix to add to the metrics in Prometheus to differentiate from other metrics in Prometheus.                                |

