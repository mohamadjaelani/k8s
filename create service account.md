### create service account
```
kubectl create sa admin2 --dry-run=client -o yaml > sa-admin2.yam
```
verify the file using
```
cat sa-admin2.yaml
```
then create it 
```
kubectl create -f sa-admin2.yaml
```
get the sa
```
kubectl get sa
```
describe sa
```
kubectl get sa-admin2 -o yaml
```
