Starting with Kubernetes version 1.24, the control plane no longer automatically creates a long-lived API token Secret for every ServiceAccount (https://discuss.kubernetes.io/t/service-account-is-getting-created-without-a-secret/14261). This change was made to improve security by shifting toward short-lived, auto-rotating tokens.\
if you want to create default secret manually the create secret yaml file
```
nano default-secret.yaml
```
and put below script
```
apiVersion: v1
kind: Secret
type: kubernetes.io/service-account-token
metadata:
  name: default-token-secret
  annotations:
    kubernetes.io/service-account.name: "default"
```
then apply
```
kubectl apply -f default-secret.yaml
```
shows the token by
```
kubectl describe secret default-token-secret
```
you'll see
```
ame:         default-token-secret
Namespace:    default
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: default
              kubernetes.io/service-account.uid: ac31c274-0a7d-49cc-965e-1057287cc81a

Type:  kubernetes.io/service-account-token

Data
====
ca.crt:     1107 bytes
namespace:  7 bytes
token:      eyJhbGciOiJSUzI1NiIsImtpZCI6IlliU3FCUm10cEdDemNCNE1XTUtWbWptSlN4N2p6dUZNdzVYVTFkVDY3dVEifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6ImRlZmF1bHQtdG9rZW4tc2VjcmV0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImRlZmF1bHQiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiJhYzMxYzI3NC0wYTdkLTQ5Y2MtOTY1ZS0xMDU3Mjg3Y2M4MWEiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6ZGVmYXVsdDpkZWZhdWx0In0.um0HFTdtI0HPfiNph31cqqseXpno0ElJ8bj2qyMTGBWJLjYEu6G8gnFgvOKNcVcVWW1gQ98rlOCfi2vWmqKV99Jg33YjgJaOQnP9IKZUrP4CxHbQ1lZ_e00iNqSqqUum2ye2M5UGQcJoC5VfwxdaPSmlf-7lY9fwm_tkQFYyZShEGyRI8A2ErkM_1UHkucsL-t7ttUdBonpZjhxjPuSM8tmuojboXjRj2vDjQGkhzGZUXK1U7_YYViiCCPHioZzNaWc7AE-sSZ-wyOVAmTHby_KrlhCXLu0YoOlViBGgZNM-7glEdeI3fa5EUvs-LTYCxVvlAzb0Qyvgdy40IN50Aw
```
or create a temporary token using below command
```
kubectl create token <service-account-name> --duration=24h

```
then attached the secret to service account:
```
kubectl patch serviceaccount admin2 -p '{"secrets": [{"name": "default-token-secret"}]}'
```
