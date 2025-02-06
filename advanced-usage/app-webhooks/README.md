# 🔗 HTTP Webhooks

Before diving into the webhooks documentation, you may want to check out [Pusher's documentation on webhooks](https://pusher.com/docs/channels/server_api/webhooks) to understand the basics of webhooks in the Pusher protocol.

## Webhook Configuration

Each [app](../../app-management/introduction.md) definition includes a `webhooks` array with structures formatted as follows:

```json
{
    "url": "string",
    "event_types": ["string", ...]
}
```

### Parameters:

| Parameter    | Type     | Description                                      |
|-------------|---------|--------------------------------------------------|
| `url`       | String  | The endpoint where the webhook data will be sent. |
| `event_types` | Array  | A list of events that will trigger the webhook. |

#### Supported `event_types`

You can specify one or more of the following event types:

- `client_event`
- `channel_occupied`
- `channel_vacated`
- `member_added`
- `member_removed`

## Webhook Payload Structure

A webhook request payload follows the same structure as [Pusher's webhook format](https://pusher.com/docs/channels/server_api/webhooks/):

```json
{
    "time_ms": 1327078148132,
    "events": [
        { "name": "event_name", "some": "data" },
        { "name": "event_name", "some": "data" }
    ]
}
```

Each event inside `events` contains:

```json
{
    "name": "client_event",
    "channel": "name of the channel the event was published on",
    "event": "name of the event",
    "data": "data associated with the event",
    "socket_id": "socket_id of the sending socket",
    "user_id": "user_id associated with the sending socket"
}
```

## Filtering Webhooks

By default, Soketi sends webhooks for all channels where the specified event types occur. You can filter webhooks to only trigger for specific channel patterns to reduce unnecessary traffic.

```json
{
    "url": "string",
    "event_types": ["channel_occupied"],
    "filter": {
        "channel_name_starts_with": "beta-",
        "channel_name_ends_with": "-app"
    }
}
```

### Example:

```javascript
// These will NOT trigger the webhook
client.subscribe('chat-room');
client.subscribe('beta-chat-room');
client.subscribe('chat-room-app');

// This WILL trigger the webhook
client.subscribe('beta-chat-room-app');
```

> **Note:** All filters use `AND` logic. If you need `OR` filtering, apply additional logic in your webhook server.

## Webhook Headers

You can define custom headers for webhook requests.

```json
{
    "url": "string",
    "event_types": ["channel_occupied"],
    "headers": {
        "X-Custom-Header": "Custom Header",
        "X-Version": "1.0"
    }
}
```

## Webhook Batching

By default, each event triggers an individual webhook request. To reduce the number of requests, enable batching using the `WEBHOOKS_BATCHING` environment variable.

```bash
SOKETI_WEBHOOKS_BATCHING=1 soketi start
```

This batches events over a **50 ms** window before sending them together in a single request. You can adjust the batching interval:

```bash
# Set batching duration to 1000ms (1 second)
SOKETI_WEBHOOKS_BATCHING=1 SOKETI_WEBHOOKS_BATCHING_DURATION=1000 soketi start
```

> **Warning:** Ensure your [graceful shutdown](../graceful-shutdowns.md#graceful-shutdown-time) duration is longer than the batching period. Otherwise, pending events may be lost during shutdown.

## Testing Webhooks

To inspect and debug webhook requests, use **Beeceptor** or an alternative tool like **Webhook.site**.

### Using Beeceptor

1. Go to [Beeceptor](https://beeceptor.com/) and create an endpoint.
2. Update your Soketi webhook URL with the Beeceptor endpoint.
3. Trigger events and inspect the received requests in Beeceptor's dashboard.

### Using Webhook.site

1. Visit [Webhook.site](https://webhook.site/) to get a temporary URL.
2. Set this as your webhook `url` in Soketi.
3. Monitor incoming requests in real time.

These tools help you verify the structure and flow of your webhook payloads before integrating them into your application.

---

