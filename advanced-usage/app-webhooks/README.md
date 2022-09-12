# 🔗 HTTP Webhooks

Before diving into the webhooks documentation, consider reading [Pusher's documentation regarding webhooks](https://pusher.com/docs/channels/server\_api/webhooks) to understand the basics of webhooks when using the Pusher protocol.

Each [app](../../app-management/introduction.md) definition contains a `webhooks` array which will contain data structures formatted like the following:

```json
{
    "url": "string",
    "event_types": ["string", ...]
}
```

* `url` - The URL where the data will be sent.
* `event_types` - An array of strings with the events that will trigger the webhook.

The value for `event_types` can be one of the following:

* `client_event`
* `channel_occupied`
* `channel_vacated`
* `member_added`
* `member_removed`

The generic look of a webhook's payload is the same as [Pusher's](https://pusher.com/docs/channels/server\_api/webhooks/):

```json
{
    "time_ms": 1327078148132,
    "events": [
        { "name": "event_name", "some": "data" },
        { "name": "event_name", "some": "data" },
        .
        .
        .
    ]
}
```

Each event from `events` looks like this:

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

### Filtering Webhooks

Enabling webhooks will send notifications for the selected `event_types`, but for all channels. In some situations, you may want to receive webhooks for specific channels, to simply reduce the network usage.

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

```javascript
// Won't trigger the webhook
client.subscribe('chat-room');
client.subscribe('beta-chat-room');
client.subscribe('chat-room-app');

// Will trigger the webhook
client.subscribe('beta-chat-room-app');
```

{% hint style="info" %}
All passed filters are combined with `AND` logic. To filter them by another logical gate like `OR`, consider filtering most of the events by passing the `filters` object and consider modifying your webhook server's code to filter them further.
{% endhint %}

### Webhook Headers

[Thanks to @stayallive's PR](https://github.com/soketi/soketi/pull/226), you can pass additional headers that will be sent within the webhook request:

```json
{
    "url": "string",
    "event_types": ["channel_occupied"],
    "headers": {
        "X-Custom-Header": "Custom Header",
        "X-Version": "Custom Header"
    }
}
```

### Webhook Batching

[Dan Pegg](https://github.com/Daynnnnn) submitted a [Pull Request](https://github.com/soketi/soketi/pull/249) that allows you to send webhooks in batches rather than on one-by-one basis. This can become useful when you don't want to send a request for each event through the webhooks, but rather give some time for more events to build up and fire all of them at once, in a single request.

To enable batching, use the `WEBHOOKS_BATCHING` environment variable:

```bash
SOKETI_WEBHOOKS_BATCHING=1 soketi start
```

The build up of events is done in `50` ms by default. On receiving an event, it waits 50 ms before sending the webhook. In those 50 ms, more events can come and build up. Once the 50 ms mark was reached, the events are being sent in one request.

If you have a lot of webhooks going on, consider increasing this value according to your needs. In the submitted [Pull Request](https://github.com/soketi/soketi/pull/249), a use case was the AWS Lambda functions webhook handling, which incurs costs based on how much the function is running and based on how many requests are done. For high-traffic apps that use those webhooks, increasing the batch duration is important, so that requests are sent at a lower rate, but with more events.

```bash
# Setting the duration to 1000ms = 1s
SOKETI_WEBHOOKS_BATCHING=1 SOKETI_WEBHOOKS_BATCHING_DURATION=1000 soketi start
```

{% hint style="warning" %}
Make sure that your [graceful shutdown](../graceful-shutdowns.md#graceful-shutdown-time) period is higher than the batch durations. If you set the batching higher than the graceful shutdown allowance, you may never receive the events that were still built up before being flushed out of the memory with the server shutdown.
{% endhint %}
