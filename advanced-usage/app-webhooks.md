# 🔗 App Webhooks

Before diving into the webhooks documentation, consider reading [Pusher's documentation regarding webhooks](https://pusher.com/docs/channels/server_api/webhooks) to understand the basics of webhooks when using the Pusher protocol.

Each [app](../app-management/introduction.md) definition contains a `webhooks` array which will contain data structures formatted like the following:

```javascript
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

