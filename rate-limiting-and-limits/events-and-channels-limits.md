# 👥 Events & Channels Limits

### HTTP REST API Limits

You can set a REST API limit at the server level. This is also known as the `hard limit`.

| Name                    | Default | Possible values    | Description                                                                                        |
| ----------------------- | ------- | ------------------ | -------------------------------------------------------------------------------------------------- |
| `HTTP_MAX_REQUEST_SIZE` | `100`   | Any number (in MB) |  The maximum size, in MB, for the total size of the request before throwing `413 Entity Too Large` |



### Events Soft Limits

Besides the rate limit, you can set soft limits for the incoming data, such as the maximum allowed event size or the maximum event name length. These ones apply globally and are called `soft limits`.

| Number                       | Default | Possible values | Description                                                                                      |
| ---------------------------- | ------- | --------------- | ------------------------------------------------------------------------------------------------ |
| `EVENT_MAX_CHANNELS_AT_ONCE` | `100`   | Any integer     | The maximum amount of channels that the client can broadcast to from a single `/events` request. |
| `EVENT_MAX_NAME_LENGTH`      | `200`   | Any integer     | The maximum length of the event name that is allowed.                                            |
| `EVENT_MAX_SIZE_IN_KB`       | `100`   | Any float       | The maximum size, in KB, for the broadcasted payloads incoming from the clients.                 |

### Channels Soft Limits

Channel interaction should be limited in some way, to prevent unwanted memory attacks with very long names. For example, the default limit for a channel name is 100 characters, but you can change it according to your needs.

| Environment variable      | Default | Possible values | Description                                                                                         |
| ------------------------- | ------- | --------------- | --------------------------------------------------------------------------------------------------- |
| `CHANNEL_MAX_NAME_LENGTH` | `100`   | Any integer     | The maximum length of the channel name that is allowed. The specific prefix names are also counted. |

### Presence Channel Limits

When dealing with the presence channels, connection details must be stored within the app. This can lead to issues if you set the limits too high and some users might abuse them on purpose, like altering their presence data to fill the memory on purpose.

There are soft limits in place for the maximum size of a member and how many members can fit into a single presence channel.

| Environment variable       | Default | Possible values | Description                                                                               |
| -------------------------- | ------- | --------------- | ----------------------------------------------------------------------------------------- |
| `PRESENCE_MAX_MEMBER_SIZE` | `10`    | Any float       | The maximum member size, in KB, for each member in a presence channel.                    |
| `PRESENCE_MAX_MEMBERS`     | `100`   | Any integer     | The maximum amount of members that can simultaneously be connected in a presence channel. |
