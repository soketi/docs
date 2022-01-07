# 🎟 Introduction

"Apps" are soketi's core authentication concept. If you are already familiar with Pusher apps, soketi "apps" serve exactly the same purpose. Namely, each "app" receives an app ID, key, and secret it may use to authenticate with the soketi server.

Apps may even be stored in MySQL or PostgreSQL for easier management of deployments with multiple apps with unique permission settings.

Within the following documentation pages, we will discuss how to configure apps for each of the supported app storage drivers. The driver that soketi uses for app management and retrieval may be defined using the following [environment variable](../getting-started/environment-variables.md):

### Environment Variables

| Name                 | Default | Possible values                          | Description                          |
| -------------------- | ------- | ---------------------------------------- | ------------------------------------ |
| `APP_MANAGER_DRIVER` | `array` | `array`, `dynamodb`, `mysql`, `postgres` | The driver used to retrieve the app. |
