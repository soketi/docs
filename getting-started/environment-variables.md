# 💿 Environment Variables

You may declare the parameters using environment variables directly passed in the CLI or at the OS level, or as key-value attributes in an `.env` file that is placed at the location from where the command is being run.

For example, either by running the command with injected variables at the CLI level or having an .env file with declared variables is either a good way.

Injecting at the CLI level:

```bash
DEBUG=1 pws-server start
```

Having a separate .env file:

```text
# Within your .env file
PWS_DEBUG=1
```

```text
pws-server start
```



