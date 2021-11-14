# Docker

When running with Docker, all you have to do is to find the right image you want to install:

```bash
docker run -p 6001:6001 quay.io/soketi/soketi:0.13-16-alpine
```

Whenever a release, commit, or master merge is done, the image containing the required code to run the application in Docker is being published to `quay.io/soketi/soketi` and you will be able to use it.

The image tags are matching the following rule:

```
quay.io/soketi/soketi:[git_version]-[node_version]
```

`[git_version]` represent the version released to the Git repository. This usually is `x.x.x`, unless it's a commit or the master branch. For commit, the value is the SHA commit and for the master branch, the value is `latest`.

`[node_version]`, for now, is only `14-alpine`. This will change in the future to support multiple node versions.

The following example versions are correct:

* `1.0.0-14-alpine` (points to `1.0.0`)
* `1.0-14-alpine` (points to the latest `1.0.x`)
* `1-14-alpine` (points to the latest `1.x`)
* `latest-14-alpine` (points to the latest `master` branch)
