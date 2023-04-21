## Set up Ingress on Docker Desktop with the NGINX Ingress Controller

&nbsp;
&nbsp;

![screen-shot-overview](./ingress-controller.png)

![screen-shot-services](./all-services.png)

### 1. Enable K8s on Docker Desktop backed by WSL2

&nbsp;
&nbsp;

### 2. Install the NGINX Ingress controller

&nbsp;
&nbsp;

check out the latest version here: https://github.com/kubernetes/ingress-nginx

&nbsp;
&nbsp;

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.3.0/deploy/static/provider/cloud/deploy.yaml

&nbsp;
&nbsp;

### 3. Check the Ingress controller pod is running

&nbsp;
&nbsp;

kubectl get pods --namespace ingress-nginx

&nbsp;
&nbsp;

### 4. Check the NGINX Ingress controller has been assigned a public Ip address

&nbsp;
&nbsp;

kubectl get service ingress-nginx-controller --namespace=ingress-nginx

&nbsp;
&nbsp;

### 5. Set up two web apps

&nbsp;
&nbsp;

kubectl apply -f aks-helloworld-one.yaml --namespace ingress-nginx

&nbsp;

kubectl apply -f aks-helloworld-two.yaml --namespace ingress-nginx

&nbsp;
&nbsp;

### 6. Setup the Ingress to route traffic between the two apps

&nbsp;
&nbsp;

kubectl apply -f hello-world-ingress.yaml --namespace ingress-nginx

&nbsp;
&nbsp;

### 7. Browse to the EXTERNAL-IP/hello-world-one and EXTERNAL-IP/hello-world-one

&nbsp;
&nbsp;

EXTERNAL-IP is localhost

&nbsp;
&nbsp;

![screen-shot-step-by-step](./command-prompt.png)

&nbsp;
&nbsp;

![screen-shot-browser](./browser.png)

&nbsp;
&nbsp;

![screen-shot-browser-2](./browser-2.png)
