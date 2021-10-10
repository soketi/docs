# 🐘 PostgreSQL

For the PostgreSQL driver, you need to configure the [PostgreSQL Database](../../databases/postgresql-configuration.md).

The table format with the mandatory fields is the following:

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

The following environment variables are available for the PostgreSQL driver:

| Name                           | Default | Possible values | Description                                                             |
| ------------------------------ | ------- | --------------- | ----------------------------------------------------------------------- |
| `APP_MANAGER_POSTGRES_TABLE`   | `apps`  | Any string      | The table name to pull the data from.                                   |
| `APP_MANAGER_POSTGRES_VERSION` | `13.3`  | Any string      | The PostgreSQL version so that the Knex connector knows how to connect. |
