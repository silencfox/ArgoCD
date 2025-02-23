# ArgoCD



## start minikube into docker
minikube start --driver=docker

### Add ingress minikube 
minikube addons enable ingress
kubectl get pods -n ingress-nginx

## Create namespace argocd
kubectl create ns argocd

## install argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.5.8/manifests/install.yaml
kubectl get all -n argocd
## expose argo cd to port 
kubectl port-forward svc/argocd-server -n argocd 8080:443
## user admin

## get credential  password 
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
## in windows powershell
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | ForEach-Object { [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($_)) }
