# 💿 Configuring the server

### Environment variables

You may declare soketi server configuration options using environment variables when invoking the soketi server directly on the CLI, or as key-value attributes in an `.env` file that is placed at the location from where the soketi server command is being run:

```bash
SOKETI_DEBUG=1 soketi start
```

Or, when using an `.env` file:

```
# Within your .env file
SOKETI_DEBUG=1
```

```
soketi start
```

Many soketi features can be controlled using environment variables, and each of these variables are discussed in the relevant sections of this documentation.

{% hint style="success" %}
To get started creating your own app credentials, visit the [Array Driver app manager.](../app-management/array-driver.md)
{% endhint %}

### File configuration

You can define a JSON-formatted file which can contain dot-formatted values for your configuration:

```json
{
    "debug": true,
    "port": 6002,
    "appManager.array.apps": [
        {
            "id": "some-id",
            "key": "some-key",
            "secret": "some-secret",
            "webhooks": [
                {
                    "url": "https://...",
                    "event_types": ["channel_occupied"]
                }
            ]
        }
    ]
}
```

```bash
soketi start --config=/path/to/config.json
```

The full list of available options can be found in the [`Options` interface](https://github.com/soketi/soketi/blob/master/src/options.ts).
