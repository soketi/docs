# 🐘 PostgreSQL

When using the PostgreSQL app driver, first configure your PostgreSQL connection credentials using [environment variables](../getting-started/environment-variables.md):

| Name                   | Default     | Possible values | Description                                         |
| ---------------------- | ----------- | --------------- | --------------------------------------------------- |
| `DB_POSTGRES_HOST`     | `127.0.0.1` | Any string      | The PostgreSQL host.     |
| `DB_POSTGRES_PORT`     | `3306`      | Any integer     | The PostgreSQL port.     |
| `DB_POSTGRES_USERNAME` | `root`      | Any string      | The PostgreSQL username. |
| `DB_POSTGRES_PASSWORD` | `password`  | Any string      | The PostgreSQL password. |
| `DB_POSTGRES_DATABASE` | `main`      | Any string      | The PostgreSQL database. |

{% hint style="success" %}
This database supports [database connection pooling](database-pooling.md).
{% endhint %}

Once you have configured your PostgreSQL database credentials, you should create a table with the following structure:

```
CREATE TABLE IF NOT EXISTS apps (
    id varchar(255) PRIMARY KEY,
    "key" varchar(255) NOT NULL,
    secret varchar(255) NOT NULL,
    max_connections integer NOT NULL,
    enable_client_messages smallint NOT NULL,
    "enabled" smallint NOT NULL,
    max_backend_events_per_sec integer NOT NULL,
    max_client_events_per_sec integer NOT NULL,
    max_read_req_per_sec integer NOT NULL,
    webhooks json
);
```

### Environment Variables

The following environment variables are used to define the behavior of the PostgreSQL app driver:

| Name                           | Default | Possible values | Description                                                             |
| ------------------------------ | ------- | --------------- | ----------------------------------------------------------------------- |
| `APP_MANAGER_POSTGRES_TABLE`   | `apps`  | Any string      | The table to pull the app data from.                                   |
| `APP_MANAGER_POSTGRES_VERSION` | `13.3`  | Any string      | The PostgreSQL version (utilized by the underlying Knex database abstraction layer). |
