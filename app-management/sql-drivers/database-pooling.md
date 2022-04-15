# ⛲ Database Pooling

Behind the scenes, connections to relational databases are made using [Knex](https://knexjs.org). If you would like to use connection pooling when connecting to your database instead of creating a new connection for each statement, you may instruct Knex to do so:

### Environment Variables

| Name                        | Default | Possible values | Description                                                                                                           |
| --------------------------- | ------- | --------------- | --------------------------------------------------------------------------------------------------------------------- |
| `SOKETI_DB_POOLING_ENABLED` | `false` | `true`, `false` | Whether to enable database connection pooling. Pooling will only be enabled if the database supports pooling in Knex. |
| `SOKETI_DB_POOLING_MIN`     | `0`     | Any number      | The minimum number of connections.                                                                                    |
| `SOKETI_DB_POOLING_MAX`     | `7`     | Any number      | The maximum number of connections.                                                                                    |
