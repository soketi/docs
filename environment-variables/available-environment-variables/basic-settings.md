# Basic Settings

### Server Settings

The configuration needed to specify the protocol, port, and host for the server.

| Name | Default | Possible values | Description |
| :--- | :--- | :--- | :--- |
| `PORT` | `6001` | Any number | The host which will be used for both the REST API and the WebSocket server. |
| `DEBUG` | `false` | `true`, `false` | Wheteher the app should be in debug mode, being very verbose with what happens behind the scenes. |

### Node Metadata

Node settings include assigning identifiers for the running node.

| Name | Default | Available values | Description |
| :--- | :--- | :--- | :--- |
| `NODE_ID` | random UUIDv4 string | Any string | An unique ID given to the node in which the process runs. Used by other features to label data. |
| `POD_ID` | `null` | Any string | The Pod name if the app runs in Kubernetes. Used by other features to label data. |

### SSL Settings

Setting one of the following variables will create an SSL version of the app.

| Name | Default | Possible values | Description |
| :--- | :--- | :--- | :--- |
| `SSL_CERT` | `''` | File paths | The path for the SSL certificate file. |
| `SSL_KEY` | `''` | File paths | The path for the SSL key file. |
| `SSL_PASS` | `''` | File path | The passphrase \(if any\) for the SSL key file to decrypt. |

### HTTP REST API

| Name | Default | Possible values | Description |
| :--- | :--- | :--- | :--- |
| `HTTP_MAX_REQUEST_SIZE` | `100` | Any number \(in MB\) |  The maximum size, in MB, for the total size of the request before throwing `413 Entity Too Large` |

### Adapter Settings

For local, single-instance applications, the default local adapter is fine.

However, when running at scale, Redis is needed to run on multiple instances or processes at the same time to ensure availability.

| Name | Default | Possible values | Description |
| :--- | :--- | :--- | :--- |
| `ADAPTER_DRIVER` | `local` | `redis`, `local` | The adapter driver to use to store and retrieve each app with channels' persistent data. |
| `ADAPTER_REDIS_PREFIX` | `''` | Any string | The Redis adapter's Pub/Sub channels prefix. |



