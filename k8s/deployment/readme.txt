## Create namespace apps
kubectl create ns apps

#### deployment 01
kubectl apply -f .\k8s\deployment\nginx2.yml --namespace apps
kubectl get pods --namespace apps
minikube service nginx-deployment -n apps --url

#### deployment 02
kubectl apply -f .\k8s\deployment\mypvc.yaml --namespace apps
kubectl apply -f .\k8s\deployment\nginx.yml --namespace apps
kubectl get pods --namespace apps
###  create service nodeport No needed, ya integrado en el deployment
###  kubectl expose deployment nginx-deployment --type=NodePort --port=8090
minikube service nginx-deployment -n apps --url

### get logs and status
kubectl get pods --selector=app=nginx-deployment -n apps
kubectl get pods -n <namespace>
kubectl get pods -n apps

kubectl logs <nombre-del-pod> -n <namespace>
kubectl logs -l app=<nombre-del-deployment> -n <namespace> --tail=100 -f
kubectl logs <nombre-del-pod> -p -n <namespace>




### eliminar servicios ETC...
kubectl delete all -l app=<nombre-del-deployment> -n <namespace>
kubectl delete all -l app=nginx-project -n <namespace>
kubectl delete replicaset -l app=<nombre-del-deployment> -n <namespace>
kubectl delete deployment nginx-project --cascade=orphan -n default
kubectl delete replicaset -l app=nginx-project -n default




####  EXAMPLE PUBLIC DEPLOYMENT AND NODE PORT  #####
kubectl create deployment hello-minikube1 --image=kicbase/echo-server:1.0
kubectl expose deployment hello-minikube1 --type=NodePort --port=8080
minikube service hello-minikube1 --url
kubectl get service hello-minikube1 --output='jsonpath="{.spec.ports[0].nodePort}"'


####  EXAMPLE PUBLIC DEPLOYMENT AND LOAD BALANCER   #####
kubectl create deployment hello-minikube1 --image=kicbase/echo-server:1.0
kubectl expose deployment hello-minikube1 --type=LoadBalancer --port=8080
minikube tunnel
kubectl get svc


### clean
minikube tunnel --cleanup