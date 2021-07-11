# 📈 Scraping Prometheus Metrics

You can enable the server to expose a `/metrics` endpoint at the given `6001` port by using the `METRICS_ENABLED` environment variable.

```bash
METRICS_ENABLED=1 pws-server start
```

```bash
curl http://127.0.0.1:6001/metrics
```

This is just a trimmed output. The exposed metrics are for both pWS connections and apps, as well as the Node.js built-in Prometheus metrics regarding the running processes, memory and CPU usage that can be quite useful for autoscaling or monitoring the running instance.

```text
# HELP pws_6001_connected The number of currently connected sockets.
# TYPE pws_6001_connected gauge

# HELP pws_6001_new_connections_total Total amount of pWS connection requests.
# TYPE pws_6001_new_connections_total counter

# HELP pws_6001_new_disconnections_total Total amount of pWS disconnections.
# TYPE pws_6001_new_disconnections_total counter

# HELP pws_6001_socket_received_bytes Total amount of bytes that pWS received.
# TYPE pws_6001_socket_received_bytes counter

# HELP pws_6001_socket_transmitted_bytes Total amount of bytes that pWS transmitted.       
# TYPE pws_6001_socket_transmitted_bytes counter

# HELP pws_6001_http_received_bytes Total amount of bytes that pWS's REST API received.    
# TYPE pws_6001_http_received_bytes counter

# HELP pws_6001_http_transmitted_bytes Total amount of bytes that pWS's REST API sent back.
# TYPE pws_6001_http_transmitted_bytes counter

...
```

