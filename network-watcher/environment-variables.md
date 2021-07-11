# 💿 Environment Variables

In the previous [Installation](installation.md#kubernetes-yaml) page that explained how to configure your workload template \(exemplified as a Deployment\), environment variables were used to tweak the Network Watcher.

The following list exposes the available variables you can use:

| Name | CLI Flag | Default | Description |
| :--- | :--- | :--- | :--- |
| `POD_NAMESPACE` | `--pod-namespace` | `default` | The Pod namespce to watch. |
| `POD_NAME` | `--pod-name` | `some-pod` | The Pod name to watch. |
| `SERVER_PORT` | `--server-port` | `6001` | The port number for the [pWS server](https://github.com/soketi/pws). |
| `MEMORY_PERCENT` | `--memory-percent` | `75` | The threshold \(in percent\) that, once reached, the Pod will be marked as "not ready" to evict any new connections or requests. |
| `CHECKING_INTERVAL` | `--checking-interval` | `1` | The number of seconds to wait between API checks. |
| `TEST_MODE` | `--test` | Not applied | Run a single check rather than a continuous loop of checks. |



