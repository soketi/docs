# 🚀 Installation

Network Watcher is available as a Docker container. It can be either installed manually by adding a container in your pods that also run pWS, or you can use the [soketi/pws Helm Chart](https://github.com/soketi/charts/tree/master/charts/pws) which comes out of the box with an already-set Network Watcher container you can easily turn on or off.

Whenever a new Github version is released, a Docker image with the same tag is being pushed to the [soketi/network-watcher](https://hub.docker.com/r/soketi/network-watcher) registry. You may check there the available tags.

### Helm Chart

To deploy using Helm, consider reading the documentation on [the pWS chart repository](https://github.com/soketi/charts/tree/master/charts/pws).

### Kubernetes YAML

The following example states how you should basically set the Network Watcher container in your pods that run pWS.

{% tabs %}
{% tab title="Service" %}
```yaml
apiVersion: v1
kind: Service
metadata:
  name: pws-service
spec:
  selector:
    app: pws
    pws.soketi.app/accepts-new-connections: "yes" # required
  ports:
    - protocol: TCP
      port: 6001
      targetPort: 6001
      name: pws
```
{% endtab %}

{% tab title="Deployment" %}
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: pws
  labels:
    app: pws
spec:
  replicas: 3
  selector:
    matchLabels:
      app: pws
  template:
    metadata:
      labels:
        app: pws
        pws.soketi.app/accepts-new-connections: "yes" # optional
    spec:
      containers:
        - name: pws
          image: soketi/pws:latest-14-alpine
          ports:
            - containerPort: 6001
        - name: network-watcher
          image: quay.io/soketi/network-watcher:4.2
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
