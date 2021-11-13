# 🛢 SQL Drivers

SQL Drivers are an abstraction that connects directly to the SQL servers and queries from a specific database and table directly, without using a third-party API.

Behind the scenes, soketi uses [Knex](https://knexjs.org) to connect to relational databases and pull the needed data.

Each table should have a specific format, in which the fields indicated for each one are mandatory. Optionally, you might append data to it if you need to, but soketi will extract only the necessary fields.
