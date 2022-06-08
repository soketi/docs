# 🧬 Array Driver

The default app driver used by soketi is the `array` driver. This is a static, in-memory array of app credentials that is kept in memory while the underlying uWS Server process is running. Whenever a connection is made or an event is broadcast, the app credentials will be verified against these in-memory credentials.

By default, default values are defined for the app ID, key, and secret for ease of installation and development. However, you should change these credentials before launching your application in production.

For rate limits and max connections options, setting the variable value to `-1` will disable the rate limits and / or max allowed connections.

### Environment Variables

| Name                                            | Default      | Possible values                                            | Description                                                                                                                                                                                |
| ----------------------------------------------- | ------------ | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `SOKETI_DEFAULT_APP_ID`                         | `app-id`     | Any string                                                 | The default app id for the array driver.                                                                                                                                                   |
| `SOKETI_DEFAULT_APP_KEY`                        | `app-key`    | Any string                                                 | The default app key for the array driver.                                                                                                                                                  |
| `SOKETI_DEFAULT_APP_SECRET`                     | `app-secret` | Any string                                                 | The default app secret for the array driver.                                                                                                                                               |
| `SOKETI_DEFAULT_APP_MAX_CONNS`                  | `-1`         | Any integer                                                | The default app's limit of concurrent connections.                                                                                                                                         |
| `SOKETI_DEFAULT_APP_ENABLE_CLIENT_MESSAGES`     | `false`      | `true`, `false`                                            | Whether client messages should be enabled for the app.                                                                                                                                     |
| `SOKETI_DEFAULT_APP_ENABLED`                    | `true`       | `true`, `false`                                            | Whether the app is activated. This option can be used to disable an app.                                                                                                                   |
| `SOKETI_DEFAULT_APP_MAX_BACKEND_EVENTS_PER_SEC` | `-1`         | Any integer                                                | The default app's limit of `/events` endpoint events broadcast per second. You can [configure rate limiting database store](../rate-limiting-and-limits/broadcast-rate-limiting.md)        |
| `SOKETI_DEFAULT_APP_MAX_CLIENT_EVENTS_PER_SEC`  | `-1`         | Any integer                                                | The default app's limit of client events broadcast per second by a single socket. You can [configure rate limiting database store](../rate-limiting-and-limits/broadcast-rate-limiting.md) |
| `SOKETI_DEFAULT_APP_MAX_READ_REQ_PER_SEC`       | `-1`         | Any integer                                                | The default app's limit of read endpoint calls per second. You can [configure rate limiting database store](../rate-limiting-and-limits/broadcast-rate-limiting.md)                        |
| `SOKETI_DEFAULT_APP_WEBHOOKS`                   | `[]`         | `[{"url": "string", "event_types": ["string", ...]}, ...]` | The webhooks list for the app. See below                                                                                                                                                   |
| `DEFAULT_APP_USER_AUTHENTICATION`               | `false`      | `true`, `false`                                            | Enable/disable the [user authentication ](../advanced-usage/user-authentication.md)feature.                                                                                                |

### App-level Limits

The `array` driver does not support setting limits at the app-level variables using environment variables. However, you can use [configuration files](../getting-started/environment-variables.md#file-configuration) to set limits for your apps:

```json
{
    "appManager.array.apps": [
        {
            "id": "app-id",
            "key": "app-key",
            "secret": "app-secret",
            "enabled": true,
            "enableClientMessages": true,
            "webhooks": [],
            "maxBackendEventsPerSecond": -1,
            "maxClientEventsPerSecond": -1,
            "maxReadRequestsPerSecond": -1,
            "maxPresenceMembersPerChannel": 100,
            "maxPresenceMemberSizeInKb": 2,
            "maxChannelNameLength": 200,
            "maxEventChannelsAtOnce": 10,
            "maxEventNameLength": 100,
            "maxEventPayloadInKb": 4,
            "maxEventBatchSize": 10
        }
    ]
}
```

{% hint style="info" %}
Keep in mind, the fields are optional and you can omit them in case you want to keep the default ones defined with the [events & channels limits environment variables](../rate-limiting-and-limits/events-and-channels-limits.md).
{% endhint %}
