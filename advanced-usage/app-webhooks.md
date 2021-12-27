# 🔗 App Webhooks

Before diving into the webhooks documentation, consider reading [Pusher's documentation regarding webhooks](https://pusher.com/docs/channels/server_api/webhooks) to understand the basics of webhooks when using the Pusher protocol.

Each [app](../app-management/introduction.md) definition contains a `webhooks` array which will contain data structures formatted like the following:

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

### Filtering Webhooks

Enabling webhooks will send notifications for the selected `event_types`, but for all channels. In some situations, you may want to receive webhooks for specific channels, to simply reduce the network usage.

Starting with soketi `0.23`, you can filter those channels you want to receive based on their name.

```json
{
    "url": "string",
    "event_types": ["channel_occupied"],
    "filters": {
        "channel_name_starts_with": "beta-",
        "channel_name_ends_with": "-app"
    }
}
```

```js
// Won't trigger the webhook
client.subscribe('chat-room');
client.subscribe('beta-chat-room');
client.subscribe('chat-room-app');

// Will trigger the webhook
client.subscribe('beta-chat-room-app');
```

{% hint style="info" %}
All passed filters are combined with `AND` logic. To filter them by another logical gate like `OR`, consider filtering the most by passing the `filters` object and consider modifying your webhook server's code to filter them further.
{% endhint %}