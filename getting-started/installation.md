# 🚀 Installation

pWS is available as CLI or as a Docker container, bringing full flexibility to run in the environment you wish.

### 💲 CLI Installation

Install is done via NPM or Yarn CLI:

```bash
npm install -g @soketi/pws
```

```bash
yarn global add @soketi/pws
```

To start the sample server, run:

```text
pws-server start
```

### 🐋 Docker Installation

When running with Docker, all you have to do is to find the right image you want to install:

```bash
docker run -p 6001:6001 soketi/pws:1.0.0-14-alpine
```

Whenever a release, commit, or master merge is done, the image containing the required code to run the application in Docker is being published to `soketi/pws` and you will be able to use it.

The image tags are matching the following rule:

```text
soketi/pws:[git_version]-[node_version]
```

`[git_version]` represent the version released to the Git repository. This usually is `x.x.x`, unless it's a commit or the master branch. For commit, the value is the SHA commit and for the master branch, the value is `latest`.

`[node_version]`, for now, is only `14-alpine`. This will change in the future to support multiple node versions.

The following example versions are correct:

* `1.0.0-14-alpine` \(points to `1.0.0`\)
* `1.0-14-alpine` \(points to the latest `1.0.x`\)
* `1-14-alpine` \(points to the latest `1.x`\)
* `latest-14-alpine` \(points to the latest `master` branch\)

### ⚓ Helm Chart Installation

pWS is also available as a Helm Chart to deploy in Kubernetes environments. The installation details and the chart are available in a separate repository called [charts/pws](https://github.com/soketi/charts/tree/master/charts/pws). You will find complete installation steps to configure and run the app in any Kubernetes cluster.

