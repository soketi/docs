# Laravel Sail (Docker)

For Laravel Sail, you might use the [Docker](docker.md) containers and add a new service in your `docker-compose.yaml` file:

```yaml
# For more information: https://laravel.com/docs/sail
version: '3'
services:
    # ...

    pws:
        image: 'quay.io/soketi/pws:latest-16-alpine'
        environment:
            DEBUG: '1'
        ports:
            - '${PWS_PORT:-6001}:6001'
        networks:
            - sail

networks:
    sail:
        driver: bridge
```

All left to do is to configure the environment variables and to [configure the broadcasting driver](../backend-configuration/laravel-broadcasting.md):

```
PUSHER_HOST=pws
PUSHER_APP_ID=app-id
PUSHER_APP_KEY=app-key
PUSHER_APP_SECRET=app-secret
```
