# 🐬 MySQL

When using the MySQL app driver, first you should configure your MySQL connection credentials as [environment variables](https://github.com/soketi/docs/blob/0.x/app-management/getting-started/environment-variables.md):

| Name                       | Default     | Possible values | Description         |
| -------------------------- | ----------- | --------------- | ------------------- |
| `SOKETI_DB_MYSQL_HOST`     | `127.0.0.1` | Any string      | The MySQL host.     |
| `SOKETI_DB_MYSQL_PORT`     | `3306`      | Any integer     | The MySQL port.     |
| `SOKETI_DB_MYSQL_USERNAME` | `root`      | Any string      | The MySQL username. |
| `SOKETI_DB_MYSQL_PASSWORD` | `password`  | Any string      | The MySQL password. |
| `SOKETI_DB_MYSQL_DATABASE` | `main`      | Any string      | The MySQL database. |

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
    `max_presence_members_per_channel` tinyint(1) NULL,
    `max_presence_member_size_in_kb` tinyint(1) NULL,
    `max_channel_name_length` tinyint(1) NULL,
    `max_event_channels_at_once` tinyint(1) NULL,
    `max_event_name_length` tinyint(1) NULL,
    `max_event_payload_in_kb` tinyint(1) NULL,
    `max_event_batch_size` tinyint(1) NULL,
    PRIMARY KEY (`id`)
);
```

### Environment Variables

The following environment variables are used to define the behavior of the MySQL app driver:

| Name                               | Default | Possible values | Description                                                                                                    |
| ---------------------------------- | ------- | --------------- | -------------------------------------------------------------------------------------------------------------- |
| `SOKETI_APP_MANAGER_MYSQL_TABLE`   | `apps`  | Any string      | The table to pull the app data from.                                                                           |
| `SOKETI_APP_MANAGER_MYSQL_VERSION` | `8.0`   | Any string      | The MySQL version (utilized by the underlying Knex database abstraction layer).                                |
| `SOKETI_APP_MANAGER_MYSQL_USE_V2`  | `false` | `true`, `false` | **soketi 0.14+.** If you're using MySQL 8.0+ and experience authentication issues, you may enable this option. |

### Limits on an app-by-app basis

To enforce app-level limits in MySQL, there are multiple fields:

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
