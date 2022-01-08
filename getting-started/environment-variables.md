# 💿 Configuring the server

#### Environment variables

You may declare soketi server configuration options using environment variables when invoking the soketi server directly on the CLI, or as key-value attributes in an `.env` file that is placed at the location from where the soketi server command is being run:

```bash
DEBUG=1 soketi start
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

#### File configuration

Starting with soketi `0.24`, you can define a JSON-formatted file which can contain dot-formatted values for your configuration:

```json
{
    "appManager.array.apps.0.id": "some-id",
    "appManager.array.apps.0.key": "some-key",
    "appManager.array.apps.0.secret": "some-secret",
    "appManager.array.apps.0.webhooks": [{
        "url": "https://...",
        "event_types": ["channel_occupied"],
    }],
    "debug": true,
    "port": 6002
}
```

```bash
soketi start --config=/path/to/config.json
```

The full list of available options can be found in the [`Options` interface](https://github.com/soketi/soketi/blob/master/src/options.ts).