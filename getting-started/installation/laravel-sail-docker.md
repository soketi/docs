# Laravel Sail (Docker)

For Laravel Sail, you may utilize soketi's [Docker](docker.md) images by adding a new service in your `docker-compose.yaml` file:

```yaml
# For more information: https://laravel.com/docs/sail
version: '3'
services:
    # ...

    soketi:
        image: 'quay.io/soketi/soketi:latest-16-alpine'
        environment:
            SOKETI_DEBUG: '1'
            SOKETI_METRICS_SERVER_PORT: '9601'
        ports:
            - '${SOKETI_PORT:-6001}:6001'
            - '${SOKETI_METRICS_SERVER_PORT:-9601}:9601'
        networks:
            - sail

networks:
    sail:
        driver: bridge
```

After adding the server definition to your application's `docker-compose.yml` file, you should configure your broadcasting environment variables as well as [the broadcasting driver](../backend-configuration/laravel-broadcasting.md):

```
PUSHER_HOST=soketi
PUSHER_APP_ID=app-id
PUSHER_APP_KEY=app-key
PUSHER_APP_SECRET=app-secret
```

### What to do next

* [Learn how to configure Laravel Echo](../client-configuration/laravel-echo.md)
* [Learn how to configure the broadcasting driver](../backend-configuration/laravel-broadcasting.md)
* [Learn how to customize the applications' credentials for better production security](../../app-management/introduction.md)
