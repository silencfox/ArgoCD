## Create namespace argocd
kubectl create ns apps
kubectl apply -f .\k8s\deployment\mypvc.yaml --namespace apps
kubectl apply -f .\k8s\deployment\nginx.yml --namespace apps
kubectl get pods --namespace apps

kubectl expose deployment nginx-deployment --type=NodePort --port=8090