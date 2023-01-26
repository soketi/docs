# Docker

{% hint style="info" %}
Starting with 0.27, you can now also deploy soketi on ARM-based devices using Docker.
{% endhint %}

soketi is also available via pre-built Docker images. To get started, you may simply run one of our available images:

```bash
docker run -p 6001:6001 -p 9601:9601 quay.io/soketi/soketi:0.34-16-debian
```

### Environment Variables

`AppId`, `AppKey`, and `AppSecret` can be set using the following environment variables:

```env
SOKETI_DEFAULT_APP_ID=YourAppId
SOKETI_DEFAULT_APP_KEY=YourAppKey
SOKETI_DEFAULT_SECRET=YourSecret
```

### Sample `docker-compose.yml` File

```yml
services:
  soketi:
    container_name: "soketi_server"
    restart: unless-stopped
    image: "quay.io/soketi/soketi:0.34-16-debian"
    ports:
      - "6001:6001"
      - "9601:9601"
    environment:
      DEBUG: 1
      SOKETI_DEFAULT_APP_ID: app-id
      SOKETI_DEFAULT_APP_KEY: app-key
      SOKETI_DEFAULT_APP_SECRET: app-secret
    networks:
      - soketi_network

networks:
  soketi_network:
    driver: bridge
```
### Alpine-based Images

{% hint style="danger" %}
Since Alpine does not support BoringSSL, Soketi cannot serve [native SSL ](../ssl-configuration.md)through Alpine images. [Learn why](https://github.com/soketi/soketi/issues/449) and use instead the Debian-based images. You can still use your proxy SSL in front of soketi.
{% endhint %}

Whenever a release, commit, or master merge is performed on the soketi GitHub repository, an image containing the required code to run the application in Docker is published to `quay.io/soketi/soketi`.

The image tags use the following naming conventions:

```
quay.io/soketi/soketi:[git_version]-[node_version]
```

`[git_version]` represent the soketi version released to the Git repository. This usually is `x.x.x`, unless it's a commit or the master branch. For commits, the value is the SHA hash of the commit. When using the master branch image, the value is `latest`.

Currently, the only supported `[node_version]` is `16-alpine`. This will be augmented in the future with additional Node versions.

The following example versions are valid:

* `0.34.1-16-alpine` (points to `0.34.1`)
* `0.34-16-alpine` (points to the latest `0.34.x`)
* `0-16-alpine` (points to the latest `0.x`)
* `latest-16-alpine` (points to the latest `0.x` branch)

### Distroless-based Image

{% hint style="danger" %}
Since Distroless does not support BoringSSL, Soketi cannot serve [native SSL ](../ssl-configuration.md)through Alpine images. [Learn why](https://github.com/soketi/soketi/issues/449) and use instead the Debian-based images. You can still use your proxy SSL in front of soketi.
{% endhint %}

Thanks to a [pull request](https://github.com/soketi/soketi/pull/178) by community member [@nsmith5](https://github.com/nsmith5), distroless-based images are available starting with the `0.18.0` version.

> _The advantage of using a distroless container is that in the case of a remote code execution vulnerability the attacker cannot open a shell because there are no shells installed in the container. This makes an attack against the server much harder to achieve, but can also make running something like `kubectl exec <your soketi pod> -- /bin/bash` harder to debug since, again, there is no shell available within the container._

Distroless image tagging follows the same convention as the Alpine-based images, but the tags are suffixed with `-distroless` instead of `-alpine`.

```bash
docker run -p 6001:6001 quay.io/soketi/soketi:0.34-16-distroless
```

{% hint style="success" %}
We recommend using the distroless images in production to avoid any security issues involving remote code execution. However, keep in mind that debugging is not enabled and it might be harder to debug live containers / pods.
{% endhint %}
