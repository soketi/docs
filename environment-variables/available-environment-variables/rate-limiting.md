# Rate Limiting

Rate limiting is helping you limit the access for applications at the app level with [app settings, per se](app-management.md).

| Name | Default | Possible values | Description |
| :--- | :--- | :--- | :--- |
| `RATE_LIMITER_DRIVER` | `local` | `local`, `redis` | The driver used for rate limit counting. |

* `local` - Rate limiting is stored within the memory and is lost upon process exit.
* `redis` - Rate limiting is centralized in Redis using the key-value store. Recommended when having a multi-node configuration.



