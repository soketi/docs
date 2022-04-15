# 🧙♂ 🧙♂ NATS Configuration

Alternative to Redis, you may use [NATS ](https://nats.io)to communicate between node instances of soketi.

{% hint style="info" %}
These environment variables work only when `SOKETI_ADAPTER_DRIVER` is set to `nats`.
{% endhint %}

### Environment Variables

| Name                                   | Default              | Possible values                | Description                                                                                                                        |
| -------------------------------------- | -------------------- | ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| `SOKETI_ADAPTER_NATS_PREFIX`           | `''`                 | Any string                     | The NATS adapter prefix.                                                                                                           |
| `SOKETI_ADAPTER_NATS_SERVERS`          | `['127.0.0.1:4222']` | Array in JSON-formatted string | The list of servers to connect to for NATS.                                                                                        |
| `SOKETI_ADAPTER_NATS_USER`             | `null`               | Any string                     | The user used to authenticate NATS requests.                                                                                       |
| `SOKETI_ADAPTER_NATS_PASSWORD`         | `null`               | Any string                     | The password used to authenticate NATS requests.                                                                                   |
| `SOKETI_ADAPTER_NATS_TOKEN`            | `null`               | Any string                     | The JWT token used to authenticate NATS requests (as alternative to user and password).                                            |
| `SOKETI_ADAPTER_NATS_TIMEOUT`          | `10000`              | Any number (milliseconds).     | The connection timeout for NATS.                                                                                                   |
| `SOKETI_ADAPTER_NATS_REQUESTS_TIMEOUT` | `5000`               | Any number (milliseconds).     | The time to wait for cross-node requests. [See `ADAPTER_CLUSTER_REQUESTS_TIMEOUT` ](redis-configuration.md#environment-variables). |
