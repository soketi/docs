# Databases

### MySQL Configuration

The configuration needed to connect to a MySQL server.

| Name | Default | Possible values | Description |
| :--- | :--- | :--- | :--- |
| `DB_MYSQL_HOST` | `127.0.0.1` | Any string | The MySQL host used for `mysql` driver. |
| `DB_MYSQL_PORT` | `3306` | Any integer | The MySQL port used for `mysql` driver. |
| `DB_MYSQL_USERNAME` | `root` | Any string | The MySQL username used for `mysql` driver. |
| `DB_MYSQL_PASSWORD` | `password` | Any string | The MySQL password used for `mysql` driver. |
| `DB_MYSQL_DATABASE` | `main` | Any string | The MySQL database used for `mysql` driver. |

This database supports [Database Pooling](databases.md#database-pooling).

### PostgreSQL Configuration

The configuration needed to connect to a PostgreSQL server.

| Name | Default | Possible values | Description |
| :--- | :--- | :--- | :--- |
| `DB_POSTGRES_HOST` | `127.0.0.1` | Any string | The PostgreSQL host used for `postgres` driver. |
| `DB_POSTGRES_PORT` | `3306` | Any integer | The PostgreSQL port used for `postgres` driver. |
| `DB_POSTGRES_USERNAME` | `root` | Any string | The PostgreSQL username used for `postgres` driver. |
| `DB_POSTGRES_PASSWORD` | `password` | Any string | The PostgreSQL password used for `postgres` driver. |
| `DB_POSTGRES_DATABASE` | `main` | Any string | The PostgreSQL database used for `postgres` driver. |

This database supports [Database Pooling](databases.md#database-pooling).

### Redis Configuration

The configuration needed to connect to a Redis server. The configuration is heavily based on [`ioredis`](https://github.com/luin/ioredis). It is therefore recommended to check out [their documentation regarding the options](https://github.com/luin/ioredis/blob/master/API.md#new-redisport-host-options). Not all options offered by `ioredis` have been implemented. The following is a list of options made available so far:

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
| `DB_REDIS_SENTINEL_PASSWORD` | `null` | Any string | An optional password used for authentication to the Sentinels. Only for `redis` driver. |
| `DB_REDIS_INSTANCE_NAME` | `mymaster` | Any string | The name of the Redis instance to which a connection should be established through the configured Sentinel\(s\). Only for `redis` driver. |

Please be aware that configuring the Sentinel options will override some of the other options like `DB_REDIS_HOST` and `DB_REDIS_PORT`, but not `DB_REDIS_DB` or `DB_REDIS_PASSWORD` for example. More details can be found in the [`ioredis` documentation for Redis Sentinel](https://github.com/luin/ioredis#sentinel).

### Database Pooling

Behind the scenes, the connections to the relational databases are made using [Knex](https://knexjs.org/). In case you are using Connection Pooling in your database, you can instruct Knex to connect to them via pooling instead of a regular one connection per statement.

| Name | Default | Possible values | Description |  |
| :--- | :--- | :--- | :--- | :--- |
| `DB_POOLING_ENABLED` | `false` | `true`, `false` | Whether to enable the database pooling. The pooling will be enabled only if the database has support pooling in Knex. |  |
| `DB_POOLING_MIN` | `0` | Any number | The minimum amount of connections. |  |
| `DB_POOLING_MAX` | `7` | Any number | The maximum amount of connections. |  |

