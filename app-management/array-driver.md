# 🧬Array Driver

The default driver is called `array`. This is a static array in-memory that is kept while the uWS Server process is running. Whenever a connection is made or an event is broadcasted, the app credentials will be checked using this method.

Out-of-the-box, a simple application is set for quick setup. You can however change the app before launching your app in production.

In case you opt-in for another `APP_MANAGER_DRIVER`, these are the variables you can change in order to change the app settings.

For the rate limits and max connections options, setting limits to `-1` will disable the rate limits and/or max allowed connections.

| Name | Default | Possible values | Description |
| :--- | :--- | :--- | :--- |
| `DEFAULT_APP_ID` | `app-id` | Any string | The default app id for the array driver. |
| `DEFAULT_APP_KEY` | `app-key` | Any string | The default app key for the array driver. |
| `DEFAULT_APP_SECRET` | `app-secret` | Any string | The default app secret for the array driver. |
| `DEFAULT_APP_MAX_CONNS` | `-1` | Any integer | The default app's limit of concurrent connections. |
| `DEFAULT_APP_ENABLE_CLIENT_MESSAGES` | `false` | `true`, `false` | Whether client messages should be enabled for the app. |
| `DEFAULT_APP_ENABLED` | `true` | `true`, `false` | Whether the app is activated. It can be used to disable an app. |
| `DEFAULT_APP_MAX_BACKEND_EVENTS_PER_SEC` | `-1` | Any integer | The default app's limit of `/events` endpoint events broadcasted per second. You can [configure rate limiting database store](../rate-limiting-and-limits/broadcast-rate-limiting.md) |
| `DEFAULT_APP_MAX_CLIENT_EVENTS_PER_SEC` | `-1` | Any integer | The default app's limit of client events broadcasted per second, by a single socket. You can [configure rate limiting database store](../rate-limiting-and-limits/broadcast-rate-limiting.md) |
| `DEFAULT_APP_MAX_READ_REQ_PER_SEC` | `-1` | Any integer | The default app's limit of read endpoint calls per second. You can [configure rate limiting database store](../rate-limiting-and-limits/broadcast-rate-limiting.md) |
| `DEFAULT_APP_WEBHOOKS` | `[]` | `[{"url": "string", "event_types": ["string", ...]}, ...]` | The webhooks list for the app. Please look below |

For Webhooks, the available `event_types` values that can be set are explained in the webhooks section: [App Webhooks](../advanced-usage/app-webhooks.md).

* `client_event`
* `channel_occupied`
* `channel_vacated`
* `member_added`
* `member_removed`

