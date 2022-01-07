# 👥 Events & Channels Limits

### HTTP REST API Limits

General limits for the soketi REST API are defined at the server level:

| Name                    | Default | Possible values    | Description                                                                                        |
| ----------------------- | ------- | ------------------ | -------------------------------------------------------------------------------------------------- |
| `HTTP_MAX_REQUEST_SIZE` | `100`   | Any number (in MB) |  The maximum size, in MB, for the total size of the request before throwing `413 Entity Too Large` |

### Event Limits

Besides the general request size limit defined above, you may define limits for specific pieces of incoming data, such as the maximum allowed event size or the maximum event name length. These limits apply globally across all servers:

| Number                       | Default | Possible values | Description                                                                                      |
| ---------------------------- | ------- | --------------- | ------------------------------------------------------------------------------------------------ |
| `EVENT_MAX_CHANNELS_AT_ONCE` | `100`   | Any integer     | The maximum number of channels that the client can broadcast to from a single `/events` request. |
| `EVENT_MAX_NAME_LENGTH`      | `200`   | Any integer     | The maximum length of an event name.                                                             |
| `EVENT_MAX_SIZE_IN_KB`       | `100`   | Any float       | The maximum size, in KB, of broadcast payloads.                                                  |
| `EVENT_MAX_BATCH_SIZE`       | `10`    | Any integer     | The maximum amount of messages that can be sent in one `/batch_events` call.                     |

### Channel Limits

Channel interaction is often limited to prevent unwanted memory attacks using very long channel names. For example, the default limit for a channel name is 100 characters; however, you can change this limit according to your needs.

| Environment variable      | Default | Possible values | Description                                                                                 |
| ------------------------- | ------- | --------------- | --------------------------------------------------------------------------------------------|
| `CHANNEL_MAX_NAME_LENGTH` | `100`   | Any integer     | The maximum length of a channel name. Channel name prefixes are counted against this limit. |

### Presence Channel Limits

When dealing with the presence channels, connection details must also be stored. This can lead to memory issues unless proper limits are in place. By default, there are limits in place for the maximum size of a member's information details and how many members can be present within a single presence channel.

| Environment variable       | Default | Possible values | Description                                                                                      |
| -------------------------- | ------- | --------------- | ------------------------------------------------------------------------------------------------ |
| `PRESENCE_MAX_MEMBER_SIZE` | `10`    | Any float       | The maximum member data size, in KB, for each member in a presence channel.                      |
| `PRESENCE_MAX_MEMBERS`     | `100`   | Any integer     | The maximum number of members that can simultaneously be connected to a single presence channel. |
