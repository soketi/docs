# 🚀 Installation

{% hint style="info" %}
The Network Watcher is only used when deploying soketi via Kubernetes.
{% endhint %}

If you run soketi standalone in a cluster at scale, you may run into capacity issues. For example, RAM usage might be near the limit supported by your server and even if you decide to horizontally scale the servers, new connections might still come to servers that are near their memory limit.

Running the soketi Network Watcher inside the same pod will solve these issues by continuously monitoring the soketi Server Usage API, labeling the pods that get over a specified threshold with `ws.soketi.app/accepts-new-connections: "no"`, so that the services watching for the pods will ignore them.

The Network Watcher source code is available on GitHub ([soketi/network-watcher](https://github.com/soketi/network-watcher)).

### Docker Container

The Network Watcher is available as a Docker container. It can either be installed manually by adding a container in your pods that also run soketi, or you can use the [soketi/soketi Helm Chart](https://github.com/soketi/charts/tree/master/charts/soketi), which includes an already-set Network Watcher container you can easily turn on and off.

When a new Network Watcher release is created on GitHub, a Docker image with the same tag is automatically pushed to the [soketi/network-watcher](https://hub.docker.com/r/soketi/network-watcher) registry where you may view the available tags.

### Helm Chart

To deploy using Helm, please consult the documentation [the soketi Helm chart GitHub repository](https://github.com/soketi/charts/tree/master/charts/soketi).

### Kubernetes YAML

The following configuration example demonstrates how you may configure the Network Watcher container in your pods that run soketi.

{% tabs %}
{% tab title="Service" %}
```yaml
apiVersion: v1
kind: Service
metadata:
  name: soketi-service
spec:
  selector:
    app: soketi
    ws.soketi.app/accepts-new-connections: "yes" # required
  ports:
    - protocol: TCP
      port: 6001
      targetPort: 6001
      name: ws
```
{% endtab %}

{% tab title="Deployment" %}
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: soketi
  labels:
    app: soketi
spec:
  replicas: 3
  selector:
    matchLabels:
      app: soketi
  template:
    metadata:
      labels:
        app: soketi
        ws.soketi.app/accepts-new-connections: "yes" # optional
    spec:
      containers:
        - name: soketi
          image: soketi/soketi:0.17-16-alpine
          ports:
            - containerPort: 6001
        - name: network-watcher
          image: quay.io/soketi/network-watcher:6
          env:
            - name: KUBE_CONNECTION
              value: cluster
            - name: MEMORY_PERCENT
              value: "75" # if > 75% memory, reject new connections
            - name: CHECKING_INTERVAL
              value: "5" # every 5 seconds
            - name: POD_NAMESPACE
              valueFrom:
                fieldRef:
                  fieldPath: metadata.namespace
            - name: POD_NAME
              valueFrom:
                fieldRef:
                  fieldPath: metadata.name
          
```
{% endtab %}
{% endtabs %}
