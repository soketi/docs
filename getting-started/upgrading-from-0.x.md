# ⬆ Upgrading from 0.x

Soketi released as 1.x stable with various new breaking changes.

## Major Impact

### Environment variables namings

Since early releases, environment variables were standard:

```bash
DEBUG=1 ADAPTER_DRIVER=mysql soketi start
```

Environment variables can be also defined in an `.env` file and run in the same location:

```bash
echo "
DEBUG=1
ADAPTER_DRIVER=mysql
" > .env
```

```bash
soketi start
```

Unfortunately, this was a bad idea, as some users might use apps that already have .env files, like Laravel. This way, Soketi will avoid configurational conflicts if it shares the same environment variable name with another framework or app that, by chance, also uses .env files.

This is how the variables would look, and it applies to both injected and file-based declarations:

```bash
SOKETI_DEBUG=1 SOKETI_ADAPTER_DRIVER=mysql soketi start
```

## Additions

### Added cached channels

Pusher announced [cached channels](https://pusher.com/docs/channels/using\_channels/cache-channels/), a way to retrieve the last sent message to a channel upon connection. Is really useful to stay in sync with previously lost state upon reconnection.
