### ARGO CD demo:
![Image](demo2.gif)

# ARGO CD installation step by step

## 1) Install kubectl and k3d
```bash
# kubectl
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/

# k3d (install script)
curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
# verify
k3d --version
```

## 2) Create a k3d cluster

```bash
k3d cluster create argo
kubectl cluster-info --context k3d-argo
```

## 3) Install Argo CD
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

## 4) Set up port forwarding

```bash
kubectl -n argocd port-forward svc/argocd-server 8080:443 &
``` 

## 6) Get the initial admin password
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode; echo
```
- Username: admin
- Password: output of the command above

