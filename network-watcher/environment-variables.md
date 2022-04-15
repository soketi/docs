# 💿 Environment Variables

Within the [Network Watcher installation](installation.md#kubernetes-yaml) documentation, environment variables were used to configure the Network Watcher. The following list of environment variables includes all of the available variables that may be used to configure the Network Watcher:

| Name                | CLI Flag              | Default     | Description                                                                                                                              |
| ------------------- | --------------------- | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `POD_NAMESPACE`     | `--pod-namespace`     | `default`   | The Pod namespace to watch.                                                                                                              |
| `POD_NAME`          | `--pod-name`          | `some-pod`  | The Pod name to watch.                                                                                                                   |
| `SERVER_PORT`       | `--server-port`       | `6001`      | The port number of the [soketi server](https://github.com/soketi/soketi).                                                                |
| `MEMORY_PERCENT`    | `--memory-percent`    | `75`        | The threshold (percentage) that, once reached, will cause the Pod to be marked as "not ready" to accept any new connections or requests. |
| `CHECKING_INTERVAL` | `--checking-interval` | `1`         | The number of seconds to wait between API checks.                                                                                        |
| `TEST_MODE`         | `--test`              | Not applied | Run a single check rather than a continuous loop of checks.                                                                              |
