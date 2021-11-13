# 📈 Scraping Prometheus Metrics

The metrics feature allows you to store metrics at the node level. This can easily be done under the hood with Prometheus. All you need to do is to set up your own Prometheus server and make it scrap the HTTP REST API of each node that soketi runs on, on the `/metrics` endpoint.

| Name                        | Default      | Possible values | Description                                                                                                         |
| --------------------------- | ------------ | --------------- | ------------------------------------------------------------------------------------------------------------------- |
| `METRICS_ENABLED`           | `false`      | `true`, `false` | Whether to enable the metrics or not. For Prometheus, enabling it will expose a `/metrics` endpoint.                |
| `METRICS_DRIVER`            | `prometheus` | `prometheus`    | The driver used to scrap the metrics. For now, only `prometheus` is available. Soon, Pushgateway will be available. |
| `METRICS_PROMETHEUS_PREFIX` | `soketi_`    | Any string      | The prefix to add to the metrics in Prometheus to differentiate from other metrics in Prometheus.                   |

You can enable the server to expose a `/metrics` endpoint at the given `6001` port by using the `METRICS_ENABLED` environment variable.

```bash
METRICS_ENABLED=1 soketi start
```

```bash
curl http://127.0.0.1:6001/metrics
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

# HELP soketi_6001_socket_transmitted_bytes Total amount of bytes that soketi transmitted.       
# TYPE soketi_6001_socket_transmitted_bytes counter

# HELP soketi_6001_http_received_bytes Total amount of bytes that soketi's REST API received.    
# TYPE soketi_6001_http_received_bytes counter

# HELP soketi_6001_http_transmitted_bytes Total amount of bytes that soketi's REST API sent back.
# TYPE soketi_6001_http_transmitted_bytes counter

...
```
