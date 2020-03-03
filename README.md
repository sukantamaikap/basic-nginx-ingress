# basic-nginx-ingress

## Way 1
* Step 1 : prerequisites
* kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.24.1/deploy/mandatory.yaml
* Step 2: nginx controller
* kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.24.1/deploy/provider/cloud-generic.yaml
* Step 3: kubectl apply -f cafe.yaml
* Step 4: kubectl apply -f cafe-ing.yaml

## Way 2
* Step 0: kubectl create -f ns.yaml 
* Step 1: helm install pub-ing stable/nginx-ingress --namespace ingress-nginx
* Step 2: kubectl apply -f cafe.yaml
* Step 3: kubectl apply -f cafe-ing.yaml
### Observation:
* On GKE, the ingress resource does not get an external ip, but the services are accessible via the public ip of the ingress controller

## Way 3
* Step 1: helm install pri-ing stable/nginx-ingress --set controller.service.annotations."cloud\.google\.com/load-balancer-type"="Internal" --namespace ingress-nginx
* Step 2: kubectl apply -f cafe.yaml
* Step 3: kubectl apply -f cafe-ing.yaml
### Observation:
* works with private network, but the IPs are different for nginx controller and ingress controller