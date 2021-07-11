# 🐬 MySQL

For the MySQL driver, you need to configure the [MySQL Database](../../environment-variables/available-environment-variables/databases.md#mysql-configuration).

The table format with the mandatory fields is the following:

```text
CREATE TABLE IF NOT EXISTS `apps` (
    `id` varchar(255) NOT NULL,
    `key` varchar(255) NOT NULL,
    `secret` varchar(255) NOT NULL,
    `max_connections` integer(10) NOT NULL,
    `enable_stats` tinyint(1) NOT NULL,
    `enable_client_messages` tinyint(1) NOT NULL,
    `max_backend_events_per_sec` integer(10) NOT NULL,
    `max_client_events_per_sec` integer(10) NOT NULL,
    `max_read_req_per_sec` integer(10) NOT NULL,
    `webhooks` json,
    PRIMARY KEY (`id`)
);
```

