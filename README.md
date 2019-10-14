# kubernetes-mattermost-install
How to install mattermost on kubernetes

Follow this [manual](https://docs.mattermost.com/install/install-kubernetes.html), with the following changes:
1. Ingress is not mandatory, can completely skip it easily
2. May require to label nodes with "kubernetes.io/os=linux"
3. If `ingress` is not installed, use the following manifest to install mattermost:
```yaml
apiVersion: mattermost.com/v1alpha1
kind: ClusterInstallation
metadata:
  name: mm-example-full
spec:
  useServiceLoadBalancer: true
  ingressName: example.mattermost-example.com
  size: 100users
  version: 5.14.0
  database:
    storageSize: 1Gi
  minio:
    storageSize: 1Gi
```
Pay attention to
```yaml
  useServiceLoadBalancer: true
```
and, surprisingly
```yaml
  ingressName: example.mattermost-example.com
```
is still required, because it is used in mattermost's Settings

Fetch URL from Service specification and enjoy!


