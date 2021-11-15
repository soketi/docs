# 🎟 Introduction

Apps are the core authentication module for soketi, as you already are familiar with Pusher apps. The concepts are the same.

Apps can be defined at the configuration level or can be pulled from a third-party API, such as MySQL or PostgreSQL for better management of who can access the WebSockets server and who can publish the events.

In this document, you will have a small insight about how you can configure your own apps, as well as how to leverage the official ecosystem apps to get started easily. The current implemented ways of App Management are pretty rigid, but in the near future we will be making them be much more flexible, such as letting the schema be customized.

### Environment Variables

| Name                 | Default | Possible values                          | Description                          |
| -------------------- | ------- | ---------------------------------------- | ------------------------------------ |
| `APP_MANAGER_DRIVER` | `array` | `array`, `dynamodb`, `mysql`, `postgres` | The driver used to retrieve the app. |
