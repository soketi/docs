# 🧠 Redis Configuration

The configuration is heavily based on [`ioredis`](https://github.com/luin/ioredis). It is therefore recommended to check out [their documentation regarding the options](https://github.com/luin/ioredis/blob/master/API.md#new-redisport-host-options). Not all options offered by `ioredis` have been implemented. The following is a list of options made available so far:

| Name | Default | Possible values | Description |
| :--- | :--- | :--- | :--- |
| `DB_REDIS_HOST` | `127.0.0.1` | Any string | The Redis host used for `redis` driver. |
| `DB_REDIS_PORT` | `6379` | Any integer | The Redis port used for `redis` driver. |
| `DB_REDIS_DB` | `0` | Any integer | The Redis database used for `redis` driver. |
| `DB_REDIS_USERNAME` | `null` | Any string | The Redis username used for authentication for `redis` driver. |
| `DB_REDIS_PASSWORD` | `null` | Any string | The Redis password used for authentication for `redis` driver. |
| `DB_REDIS_PREFIX` | `pws` | Any string | The key prefix for Redis. Only for the`redis` driver. |

The following options are available when connecting to Redis through one or more Sentinels:

| Name | Default | Possible values | Description |
| :--- | :--- | :--- | :--- |
| `DB_REDIS_SENTINELS` | `null` | Any string | A JSON-encoded array of objects with `host` and `port` of Sentinels to connect to. Only for the `redis` driver. |
| `DB_REDIS_SENTINEL_PASSWORD` | `null` | Any string | The \(optional\) password that is used to authenticate to the Sentinels. Only for `redis` driver. |
| `DB_REDIS_INSTANCE_NAME` | `mymaster` | Any string | The name of the Redis instance to which a connection should be established through the configured Sentinel\(s\). Only for `redis` driver. |

Please be aware that configuring the Sentinel options will override some of the other options like `DB_REDIS_HOST` and `DB_REDIS_PORT`, but not `DB_REDIS_DB` or `DB_REDIS_PASSWORD` for example. More details can be found in the [`ioredis` documentation for Redis Sentinel](https://github.com/luin/ioredis#sentinel).

