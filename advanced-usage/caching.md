# 📝 Caching

Soketi has a caching layer built within. This allows you to speed up some processes like app retrievals or to use it as a centralized storage for read-write intensive tasks.

Currently, the caching system is used to [cache app retrievals](../app-management/introduction.md#caching-app-retrievals) (if enabled) or store the cache for [Cached Channels](https://blog.pusher.com/introducing-cache-channels/) when scaling across multiple nodes.

| Name                       | Default  | Possible values   | Description                                                                                                         |
| -------------------------- | -------- | ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| `SOKETI_CACHE_DRIVER`      | `memory` | `memory`, `redis` | The caching driver.                                                                                                 |
| `CACHE_REDIS_CLUSTER_MODE` | `false`  | `false`, `true`   | Enable this if you run Redis in Cluster mode. [Read more](../getting-started/redis-configuration.md#redis-cluster). |
