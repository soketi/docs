# App Management

### Default Application

Out-of-the-box, a simple application is set for quick setup. You can however change the app before launching your app in production.

In case you opt-in for another `APP_MANAGER_DRIVER`, these are the variables you can change in order to change the app settings.

For the rate limits and max connections options, setting limits to `-1` will disable the rate limits and/or max allowed connections.

| Name | Default | Possible values | Description |
| :--- | :--- | :--- | :--- |
| `DEFAULT_APP_ID` | `app-id` | Any string | The default app id for the array driver. |
| `DEFAULT_APP_KEY` | `app-key` | Any string | The default app key for the array driver. |
| `DEFAULT_APP_SECRET` | `app-secret` | Any string | The default app secret for the array driver. |
| `DEFAULT_APP_MAX_CONNS` | `-1` | Any integer | The default app's limit of concurrent connections. |
| `DEFAULT_APP_ENABLE_CLIENT_MESSAGES` | `false` | `true`, `false` | Wether client messages should be enabled for the app. |
| `DEFAULT_APP_MAX_BACKEND_EVENTS_PER_SEC` | `-1` | Any integer | The default app's limit of `/events` endpoint events broadcasted per second. You can [configure rate limiting database store](rate-limiting.md) |
| `DEFAULT_APP_MAX_CLIENT_EVENTS_PER_SEC` | `-1` | Any interger | The default app's limit of client events broadcasted per second, by a single socket. You can [configure rate limiting database store](rate-limiting.md) |
| `DEFAULT_APP_MAX_READ_REQ_PER_SEC` | `-1` | Any integer | The default app's limit of read endpoint calls per second. You can [configure rate limiting database store](rate-limiting.md) |
| `DEFAULT_APP_WEBHOOKS` | `[]` | `[{"url": "string", "event_types": ["string", ...]}, ...]` | The webhooks list for the app. Please look below |

For Webhooks, the available `event_types` values that can be set are listed below. Consider reading more about webhooks in [App Webhooks](../../advanced-usage/app-webhooks.md).

* `client_event`
* `channel_occupied`
* `channel_vacated`
* `member_added`
* `member_removed`

### App Managers

 The apps manager manages the allowed apps to connect to the WS and the API. Defaults to the local, `array` driver predefined by the `DEFAULT_APP_*` variables.

| Name | Default | Possible values | Description |
| :--- | :--- | :--- | :--- |
| `APP_MANAGER_DRIVER` | `array` | `array`, `dynamodb`, `mysql`, `postgres` | The driver used to retrieve the app. |

Additionally, the following settings apply for further configurations of the app manager that was selected:

| Name | Default | Possible values | Description |
| :--- | :--- | :--- | :--- |
| `APP_MANAGER_DYNAMODB_TABLE` | `apps` | Any string | The table name to pull the data from. Only for `dynamodb`. |
| `APP_MANAGER_DYNAMODB_REGION` | `us-east-1` | Any AWS region | The DynamoDB region the table was deployed in. For global tables, pick any region. Only for `dynamodb`. |
| `APP_MANAGER_DYNAMODB_ENDPOINT` | `''` | Any URL | The endpoint to connect to DynamoDB. Optional, used for testing or for local DynamoDB configurations. Only for `dynamodb`. |
| `APP_MANAGER_MYSQL_TABLE` | `apps` | Any string | The table name to pull the data from. Only for `mysql`. |
| `APP_MANAGER_MYSQL_VERSION` | `8.0` | Any string | The MySQL version so that the Knex connector knows how to connect. Only for `mysql`. |
| `APP_MANAGER_POSTGRES_TABLE` | `apps` | Any string | The table name to pull the data from. Only for `postgres`. |
| `APP_MANAGER_POSTGRES_VERSION` | `13.3` | Any string | The PostgreSQL version so that the Knex connector knows how to connect. Only for `postgres`. |

To learn more about app managers for third-party databases, please consider:

* [DynamoDB](../../app-management/dynamodb.md)
* [MySQL](../../app-management/sql-drivers/mysql.md)
* [PostgreSQL](../../app-management/sql-drivers/postgresql.md)

