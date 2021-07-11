# Prometheus Metrics

The metrics feature allows you to store metrics at the node level. This can easily be done under the hood with Prometheus. All you need to do is to set up your own Prometheus server and make it scrap the HTTP REST API of each node that pWS runs on, on the `/metrics` endpoint.

| Name | Default | Possible values | Description |
| :--- | :--- | :--- | :--- |
| `METRICS_ENABLED` | `false` | `true`, `false` | Whether to enable the metrics or not. For Prometheus, enabling it will expose a `/metrics` endpoint. |
| `METRICS_DRIVER` | `prometheus` | `prometheus` | The driver used to scrap the metrics. For now, only `prometheus` is available. Soon, Pushgateway will be available. |
| `METRICS_PROMETHEUS_PREFIX` | `pws_` | Any string | The prefix to add to the metrics in Prometheus to differentiate from other metrics in Prometheus. |



