# ✨ Getting Started

**Network Watcher works only with Kubernetes**!

If you run pWS standalone in a cluster, at scale, you might run into capacity issues: RAM usage might be near the limit and even if you decide to horizontally scale the pods, new connections might still come to pods that are near-limit and run into OOM at some point.

 Running Network Watcher inside the same pod will solve the issues by continuously checking the pWS Server Usage API, labeling the pods that get over a specified threshold with `pws.soketi.app/accepts-new-connections: "no"`, so that the services watching for the pods will ignore them. This way, the services will know not to redirect new traffic to the already almost full pods that currently manage active connections.

The source code is available at [soketi/network-watcher](https://github.com/soketi/network-watcher).

```yaml
kind: Service
metadata:
  name: pws-service
spec:
  ports:
    - port: 6001
      targetPort: 6001
      protocol: TCP
      name: pws
  selector:
    app: my-app
    pws.soketi.app/accepts-new-connections: "yes"
```

