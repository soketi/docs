# 🐬 MySQL

For the MySQL driver, you need to configure the [MySQL Database](../../databases/mysql-configuration.md).

The table format with the mandatory fields is the following:

```
CREATE TABLE IF NOT EXISTS `apps` (
    `id` varchar(255) NOT NULL,
    `key` varchar(255) NOT NULL,
    `secret` varchar(255) NOT NULL,
    `max_connections` integer(10) NOT NULL,
    `enable_client_messages` tinyint(1) NOT NULL,
    `enabled` tinyint(1) NOT NULL,
    `max_backend_events_per_sec` integer(10) NOT NULL,
    `max_client_events_per_sec` integer(10) NOT NULL,
    `max_read_req_per_sec` integer(10) NOT NULL,
    `webhooks` json,
    PRIMARY KEY (`id`)
);
```

### Environment Variables

The following environment variables are available for the MySQL driver:

| Name                        | Default | Possible values | Description                                                                                                        |
| --------------------------- | ------- | --------------- | ------------------------------------------------------------------------------------------------------------------ |
| `APP_MANAGER_MYSQL_TABLE`   | `apps`  | Any string      | The table name to pull the data from.                                                                              |
| `APP_MANAGER_MYSQL_VERSION` | `8.0`   | Any string      | The MySQL version so that the Knex connector knows how to connect.                                                 |
| `APP_MANAGER_MYSQL_USE_V2`  | `false` | `true`, `false` | **Only for soketi 0.14+.** If you're using MySQL 8.0+ and have authentication issues, fix issues by enabling this. |
