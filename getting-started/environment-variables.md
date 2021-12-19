# 💿 Environment Variables

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
