# 🐬 MySQL Configuration

The configuration that is needed to connect to a MySQL server.

| Name                | Default     | Possible values | Description                                 |
| ------------------- | ----------- | --------------- | ------------------------------------------- |
| `DB_MYSQL_HOST`     | `127.0.0.1` | Any string      | The MySQL host used for `mysql` driver.     |
| `DB_MYSQL_PORT`     | `3306`      | Any integer     | The MySQL port used for `mysql` driver.     |
| `DB_MYSQL_USERNAME` | `root`      | Any string      | The MySQL username used for `mysql` driver. |
| `DB_MYSQL_PASSWORD` | `password`  | Any string      | The MySQL password used for `mysql` driver. |
| `DB_MYSQL_DATABASE` | `main`      | Any string      | The MySQL database used for `mysql` driver. |

This database supports [Database Pooling](database-pooling.md).
