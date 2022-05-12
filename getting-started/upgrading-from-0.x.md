# ⬆ Upgrading from 0.x

Soketi released as 1.x stable with various new breaking changes.

The update time is minimal, at most 30 mins, depending on the overall complexity of your Soketi implementation.

## Major Impact

### Corking requests

Starting with 1.x, the [requests are now corked](https://github.com/soketi/soketi/pull/219).

HTTP requests can be received in small chunks before the response is actually finished, at the network level. These chunks/packets contain details about the headers, for example, and other metadata. This can be computationally hard, both CPU and network, to compress and send multiple times.

By corking, the data chunks are gathered entirely, compressed, and sent back.

Preliminary, internal tests revealed network performance slightly better than before. If you see issues in response times,&#x20;

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

To stay up-to-date with Pusher and offer the best open-source experience, we've decided to show it off as a breaking change.
