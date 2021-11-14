# 🔗 HTTP Webhooks

Before diving into the webhooks documentation, consider reading [Pusher's documentation about webhooks](https://pusher.com/docs/channels/server\_api/webhooks) to understand how this process works.

Each retrieved app contains a `webhooks` array which will contain elements formatted like this:

```javascript
{
    "url": "string",
    "event_types": ["string", ...]
}
```

* `url` - The URL where the data will be sent to
* `event_types` - an array of strings with the events that will trigger the webhook

The value for `event_types` can be one of the following:

* `client_event`
* `channel_occupied`
* `channel_vacated`
* `member_added`
* `member_removed`

