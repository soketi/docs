# 🐬 MySQL

When using the MySQL app driver, first you should configure your MySQL connection credentials as [environment variables](../getting-started/environment-variables.md):

| Name                | Default     | Possible values | Description         |
| ------------------- | ----------- | --------------- | ------------------- |
| `DB_MYSQL_HOST`     | `127.0.0.1` | Any string      | The MySQL host.     |
| `DB_MYSQL_PORT`     | `3306`      | Any integer     | The MySQL port.     |
| `DB_MYSQL_USERNAME` | `root`      | Any string      | The MySQL username. |
| `DB_MYSQL_PASSWORD` | `password`  | Any string      | The MySQL password. |
| `DB_MYSQL_DATABASE` | `main`      | Any string      | The MySQL database. |

{% hint style="success" %}
This database supports [database connection pooling](database-pooling.md).
{% endhint %}

Once you have configured your MySQL database credentials, you should create a table with the following structure:

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

The following environment variables are used to define the behavior of the MySQL app driver:

| Name                        | Default | Possible values | Description                                                                                                    |
| --------------------------- | ------- | --------------- | -------------------------------------------------------------------------------------------------------------- |
| `APP_MANAGER_MYSQL_TABLE`   | `apps`  | Any string      | The table to pull the app data from.                                                                           |
| `APP_MANAGER_MYSQL_VERSION` | `8.0`   | Any string      | The MySQL version (utilized by the underlying Knex database abstraction layer).                                |
| `APP_MANAGER_MYSQL_USE_V2`  | `false` | `true`, `false` | **soketi 0.14+.** If you're using MySQL 8.0+ and experience authentication issues, you may enable this option. |

### Limits on an app-by-app basis

This feature is truly optional. To enforce app-level limits in MySQL, you should add the following fields to your table:

```sql
`max_presence_members_per_channel` tinyint(1) NULL,
`max_presence_member_size_in_kb` tinyint(1) NULL,
`max_channel_name_length` tinyint(1) NULL,
`max_event_channels_at_once` tinyint(1) NULL,
`max_event_name_length` tinyint(1) NULL,
`max_event_payload_in_kb` tinyint(1) NULL,
`max_event_batch_size` tinyint(1) NULL
```

Setting any of them to `null` or `''` will ignore the setting, and use the limits associated [with the server-level declared defaults](../../rate-limiting-and-limits/events-and-channels-limits.md).

Existing apps running on `<0.29.0` will still work even if you don't have these fields added after the migration to `0.29.0`. You should add these fields to keep your database up-to-date or to have the choice to, later on, imply limits to your apps.
