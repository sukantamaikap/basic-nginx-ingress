# basic-nginx-ingress
A sample working nginx ingress controller for GKE.

## Way 1 - with ingress-nginx controller 
* Step 1: kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.24.1/deploy/mandatory.yaml
* Step 2: nginx controller
* kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.24.1/deploy/provider/cloud-generic.yaml
* Step 3: kubectl apply -f cafe.yaml
* Step 4: kubectl apply -f cafe-ing.yaml

## Way 2 - with nginx-ingress controller open to public
* Step 0: kubectl create -f ns.yaml 
* Step 1: helm install pub-ing stable/nginx-ingress --namespace ingress-nginx
* Step 2: kubectl apply -f cafe.yaml
* Step 3: kubectl apply -f cafe-ing.yaml

## Way 3 - with nginx-ingress controller NOT open to public
* Step 1: helm install nginx-ingress stable/nginx-ingress --namespace ingress-nginx --set controller.service.annotations."cloud\.google\.com/load-balancer-type"="Internal"
* Step 2: kubectl apply -f cafe.yaml
* Step 3: kubectl apply -f cafe-ing.yaml


#### Note:
I tested this on GKE.