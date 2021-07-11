# 🐘 PostgreSQL

For the PostgreSQL driver, you need to configure the [PostgreSQL Database](../../environment-variables/available-environment-variables/databases.md#postgresql-configuration).

The table format with the mandatory fields is the following:

```text
CREATE TABLE IF NOT EXISTS apps (
    id varchar(255) PRIMARY KEY,
    "key" varchar(255) NOT NULL,
    secret varchar(255) NOT NULL,
    max_connections integer NOT NULL,
    enable_stats smallint NOT NULL,
    enable_client_messages smallint NOT NULL,
    max_backend_events_per_sec integer NOT NULL,
    max_client_events_per_sec integer NOT NULL,
    max_read_req_per_sec integer NOT NULL,
    webhooks json
);
```

