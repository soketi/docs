# 🎟 Introduction

"Apps" are soketi's core authentication concept. If you are already familiar with Pusher apps, soketi "apps" serve exactly the same purpose. Namely, each "app" receives an app ID, key, and secret it may use to authenticate with the soketi server.

Apps may even be stored in MySQL or PostgreSQL for easier management of deployments with multiple apps with unique permission settings.

Within the following documentation pages, we will discuss how to configure apps for each of the supported app storage drivers. The driver that soketi uses for app management and retrieval may be defined using the following [environment variable](../getting-started/environment-variables.md):

### Environment Variables

| Name                        | Default | Possible values                          | Description                          |
| --------------------------- | ------- | ---------------------------------------- | ------------------------------------ |
| `SOKETI_APP_MANAGER_DRIVER` | `array` | `array`, `dynamodb`, `mysql`, `postgres` | The driver used to retrieve the app. |

### Caching app retrievals

Soketi can cache the apps that are retrieved for authentication. The apps retrieved in the cache cannot be purged until the TTL causes it to get evicted and replaced with the fresh value from the database. The caching is on a per-app basis.

{% hint style="info" %}
Please also see the [caching section](../advanced-usage/caching.md) for additional configuration.
{% endhint %}

| Name                               | Default | Possible values     | Description                                                   |
| ---------------------------------- | ------- | ------------------- | ------------------------------------------------------------- |
| `SOKETI_APP_MANAGER_CACHE_ENABLED` | `false` | `true`, `false`     | Enable temporary caching of apps in the memory.               |
| `SOKETI_APP_MANAGER_CACHE_TTL`     | `-1`    | `-1` or any integer | The TTL of cache-stored apps, in seconds. `-1` for unlimited. |
