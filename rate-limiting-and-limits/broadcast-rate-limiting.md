# ⛔ Broadcast Rate Limiting

Rate limiting helps you throttle the number of requests for client events, backend events or HTTP REST API calls for the read endpoints (like `/channels`) at the app level. This will help you have enough control over bad-intentioned users.

Setting the rate limiter driver depends on the architecture the server is deployed in. For local, single-instance servers, the default local driver is alright, but for multi-node, a third-party database is needed.

Settings for the limits are available at the app level. [Read the documentation about App Management](../app-management/introduction.md).

| Name                  | Default | Possible values  | Description                              |
| --------------------- | ------- | ---------------- | ---------------------------------------- |
| `RATE_LIMITER_DRIVER` | `local` | `local`, `redis` | The driver used for rate limit counting. |

* `local` - Rate limiting is stored within the memory and is lost upon process exit.
* `redis` - Rate limiting is centralized in Redis using the key-value store. Recommended when having a multi-node configuration.
