

### ingress minikube 
minikube addons enable ingress
kubectl get pods -n ingress-nginx
kubectl create deployment web --image=gcr.io/google-samples/hello-app:1.0
kubectl get deployment web 
kubectl expose deployment web --type=NodePort --port=8080
kubectl get service web

minikube service web --url
curl http://172.17.0.15:31637 

kubectl apply -f https://k8s.io/examples/service/networking/example-ingress.yaml
kubectl get ingress

minikube tunnel
minikube ip
### add the ip to the etc/hosts
172.17.0.15 hello-world.example


###  https://spacelift.io/blog/kubernetes-ingress
## install ingress  AKS
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.3.0/deploy/static/provider/cloud/deploy.yaml
kubectl get pods --namespace ingress-nginx
kubectl get service ingress-nginx-controller --namespace=ingress-nginx


kubectl create ingress demo --class=nginx --rule [DNS_NAME]/=demo:80