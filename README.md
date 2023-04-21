# 1. Install the NGINX Ingress controller

## kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.3.0/deploy/static/provider/cloud/deploy.yaml


# 2. Check the Ingress controller pod is running

## kubectl get pods --namespace ingress-nginx

# 3. Check the NGINX Ingress controller has been assigned a public Ip address

## kubectl get service ingress-nginx-controller --namespace=ingress-nginx

# 4. Set up two web apps

## kubectl apply -f aks-helloworld-one.yaml --namespace ingress-nginx

## kubectl apply -f aks-helloworld-two.yaml --namespace ingress-nginx

# 5. Setup the Ingress to route traffic between the two apps

## kubectl apply -f hello-world-ingress.yaml --namespace ingress-nginx

# 6. Browse to the EXTERNAL_IP/hello-world-one and EXTERNAL_IP/hello-world-one