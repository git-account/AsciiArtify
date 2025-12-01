### ARGO CD MVP:
![Image](MVP.gif)

# ARGO CD configuration - adding a new application


## 1) Set up port forwarding

```bash
kubectl -n argocd port-forward svc/argocd-server 8080:443 &
``` 

## 2) Get the initial admin password
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode; echo
```
- Username: admin
- Password: output of the command above

## 3) Click "+ NEW APP"

```bash
Example:
Application Name: demo
Project Name: default
SYNC POLICY: Automatic
SYNC OPTIONS: Auto create namespace
Repository URL: https://github.com/den-vasyliev/go-demo-app
Path: HELM
Cluster URL: https://kubernetes.default.svc
Namespace: demo

``` 

## 3) Click "CREATE"

Wait for sync to complete
