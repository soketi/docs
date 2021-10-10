# ⛲ Database Pooling

Behind the scenes, the connections to the relational databases are made using [Knex](https://knexjs.org). In case you are using Connection Pooling in your database, you can instruct Knex to connect to them via pooling instead of a regular one connection per statement.

| Name                 | Default | Possible values | Description                                                                                                           |
| -------------------- | ------- | --------------- | --------------------------------------------------------------------------------------------------------------------- |
| `DB_POOLING_ENABLED` | `false` | `true`, `false` | Whether to enable the database pooling. The pooling will be enabled only if the database has support pooling in Knex. |
| `DB_POOLING_MIN`     | `0`     | Any number      | The minimum amount of connections.                                                                                    |
| `DB_POOLING_MAX`     | `7`     | Any number      | The maximum amount of connections.                                                                                    |
