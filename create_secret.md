Starting with Kubernetes version 1.24, the control plane no longer automatically creates a long-lived API token Secret for every ServiceAccount. This change was made to improve security by shifting toward short-lived, auto-rotating tokens.\
if you want to create default secret manually the create secret yaml file and put below script
```
apiVersion: v1
kind: Secret
type: kubernetes.io/service-account-token
metadata:
  name: default-token-secret
  annotations:
    kubernetes.io/service-account.name: "default"
```
