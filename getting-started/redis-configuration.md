# 🧠 Redis Configuration

If you choose to use the Redis driver for horizontal scalability, rate-limiting data storage, or queue support, you will need to configure additional environment variables to instruct soketi on how to connect to Redis.

If you are not using Redis for rate limiting or queues, these environment variables are not required.

### Environment Variables

| Name                         | Default     | Possible values | Description                                   |
| ---------------------------- | ----------- | --------------- | --------------------------------------------- |
| `SOKETI_DB_REDIS_HOST`       | `127.0.0.1` | Any string      | The Redis host.                               |
| `SOKETI_DB_REDIS_PORT`       | `6379`      | Any integer     | The Redis port.                               |
| `SOKETI_DB_REDIS_DB`         | `0`         | Any integer     | The Redis database.                           |
| `SOKETI_DB_REDIS_USERNAME`   | `null`      | Any string      | The Redis username.                           |
| `SOKETI_DB_REDIS_PASSWORD`   | `null`      | Any string      | The Redis password.                           |
| `SOKETI_DB_REDIS_KEY_PREFIX` | `null`      | Any string      | The Redis key prefix that should be utilized. |

### Redis Sentinel

The following additional options are available when connecting to Redis through one or more Sentinels.

{% hint style="info" %}
Please be aware that utilizing the Sentinel options will override some of the other options like `DB_REDIS_HOST` and `DB_REDIS_PORT`, but not `DB_REDIS_DB` or `DB_REDIS_PASSWORD`. More details can be found in the [`ioredis` documentation for Redis Sentinel](https://github.com/luin/ioredis#sentinel).
{% endhint %}

| Name                                | Default    | Possible values | Description                                                                                                  |
| ----------------------------------- | ---------- | --------------- | ------------------------------------------------------------------------------------------------------------ |
| `SOKETI_DB_REDIS_SENTINELS`         | `null`     | Any string      | A JSON-encoded array of objects with `host` and `port` of Sentinels to connect to.                           |
| `SOKETI_DB_REDIS_SENTINEL_PASSWORD` | `null`     | Any string      | The (optional) password that is used to authenticate with the Sentinels.                                     |
| `SOKETI_DB_REDIS_INSTANCE_NAME`     | `mymaster` | Any string      | The name of the Redis instance to which a connection should be established through the configured Sentinels. |

### Redis Cluster

The following additional options are available when connecting to Redis Cluster configurations.

{% hint style="info" %}
Please be aware that utilizing the Cluster options will override some of the other options like `DB_REDIS_HOST` and `DB_REDIS_PORT`, but not `DB_REDIS_DB` or `DB_REDIS_PASSWORD`. More details can be found in the [`ioredis` documentation for Redis Cluster](https://github.com/luin/ioredis#cluster).
{% endhint %}

| Name                            | Default | Possible values | Description                                                                    |
| ------------------------------- | ------- | --------------- | ------------------------------------------------------------------------------ |
| `SOKETI_DB_REDIS_CLUSTER_NODES` | `[]`    | Any string      | A JSON-encoded array of objects with `host` and `port` of Nodes to connect to. |
