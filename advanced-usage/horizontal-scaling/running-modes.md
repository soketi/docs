# 🤖 Running Modes

When scaling, you perhaps want to decouple the webhooks queue processing from your active servers that handle WS/HTTP traffic. This brings bigger performance than the previous monolithic principle in soketi.

The app itself is full-stack, meaning it works as an HTTP API, WebSocket Server, and Queue processor, all at once. The `MODE` variable is now introduced to help you scale apps that use external drivers (like Redis for queue).

You may want to have two fleets: one that actively interacts with the userbase HTTP/WS, and one fleet that scales independently to process queues for webhooks.

### `SOKETI_MODE=full`

The default mode. Soketi acts like a processing worker and server, at the same time.

### `SOKETI_MODE=server`

It does not process queues. It will only serve HTTP/WS requests to your clients. This is the server that should expose the port to the public.

### `SOKETI_MODE=worker`

You need to pair this specific mode setting with `PORT` to choose a different port to run on.

The servers running in this mode will have an HTTP server running so that you can check for

* &#x20;`/metrics`
* `/` (health checks)
* `/ready` (readiness checks)

There are **NO** WebSocket endpoints running in this mode.
