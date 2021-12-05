# Docker

When running with Docker, all you have to do is to find the right image you want to install:

```bash
docker run -p 6001:6001 quay.io/soketi/soketi:0.17-16-alpine
```

### Alpine-based Image

Whenever a release, commit, or master merge is done, the image containing the required code to run the application in Docker is being published to `quay.io/soketi/soketi` and you will be able to use it.

The image tags are matching the following rule:

```
quay.io/soketi/soketi:[git_version]-[node_version]
```

`[git_version]` represent the version released to the Git repository. This usually is `x.x.x`, unless it's a commit or the master branch. For commit, the value is the SHA commit and for the master branch, the value is `latest`.

`[node_version]`, for now, is only `16-alpine`. This will change in the future to support multiple node versions.

The following example versions are correct:

* `0.17.1-16-alpine` (points to `0.17.1`)
* `0.17-16-alpine` (points to the latest `0.17.x`)
* `1-16-alpine` (points to the latest `1.x`)
* `latest-16-alpine` (points to the latest `master` branch)

### Distroless-based Image

Thanks to [@nsmith5](https://github.com/nsmith5) ([Pull Request](https://github.com/soketi/soketi/pull/178)), starting with `0.18.0`, Distroless-based images are also shipped.

> _The advantage of using a distroless container is that in the case of a remote code execution vulnerability the attacker cannot open a shell because there are no shells installed in the container. This makes an attack quite a bit harder to pull off, but can also make running something like `kubectl exec <your soketi pod> -- /bin/bash` to debug harder as, again, there is no shell in the container._

The tagging is the same as the Alpine-based images, but the tags are suffixed with `-distroless` instead of `-alpine`.

```bash
docker run -p 6001:6001 quay.io/soketi/soketi:0.18-16-distroless
```

{% hint style="warning" %}
It's highly encouraged to use distroless images in production to avoid any security issues with RCE. Keep in mind that debugging is not enabled and it might be harder to debug live containers/pods.
{% endhint %}
