## Set up Ingress on Docker Desktop with the NGINX Ingress Controller

&nbsp;

The following diagram (from <\<Learn K8s in a month of Lunches\>>) is for illustration purpose only.

&nbsp;

![screen-shot-overview](screen-shot/ingress-controller.png)

&nbsp;

The separation between Ingress rules (objects) and the ingress controller makes it easy to compare different reverse proxy implementations and see which gives you the combination of features and usability you're happy with.
&nbsp;

Kubernetes does let you run multiple ingress controllers, and in a complex environment, you may do that to provide different sets of capabilities for different applications.

&nbsp;

The followings are the result of setting up Nginx and Kong ingress controllers.

&nbsp;

![screen-shot-all-deployments](screen-shot/all-deployments.png)

![screen-shot-all-services](screen-shot/all-services.png)

![screen-shot-all-ingresses](screen-shot/all-ingresses.png)

### 1. Enable K8s on Docker Desktop backed by WSL2

&nbsp;
&nbsp;

![screen-shot-k8s-settings](screen-shot/docker-desktop-k8s-settings.png)

&nbsp;

To deploy and access the Kubernetes Dashboard, please refer to:

https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/

https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md

The yaml file for creating sample user is at k8s-dash-board folder.

&nbsp;

### 2. Install the NGINX Ingress controller

&nbsp;
&nbsp;

Check out the latest version here: https://github.com/kubernetes/ingress-nginx

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

### 7. Browse to the EXTERNAL-IP/, EXTERNAL-IP/hello-world-one, and EXTERNAL-IP/hello-world-one

&nbsp;
&nbsp;

EXTERNAL-IP is localhost

&nbsp;
&nbsp;

![screen-shot-step-by-step](screen-shot/command-prompt.png)

&nbsp;
&nbsp;

![screen-shot-browser](screen-shot/browser.png)

&nbsp;
&nbsp;

![screen-shot-browser-2](screen-shot/browser-2.png)

### 8. Deploy another deployment/service and ingress resource and browse to EXTERNAL-IP/kiamol

&nbsp;
&nbsp;

kubectl apply -f hello-kiamol/ --namespace ingress-nginx

&nbsp;
&nbsp;

kubectl apply -f hello-kiamol/ingress/localhost.yaml --namespace ingress-nginx

&nbsp;
&nbsp;

![screen-shot-ingress-2](screen-shot/another-ingress-for-kiamol.png)


### 9. Deploy Kong as an additional ingress controller in the cluster

&nbsp;

Adapted from Kong Ingress on Minikube (https://docs.konghq.com/kubernetes-ingress-controller/2.9.x/deployment/minikube). The kong-proxy port was changed from 80 to 8000.

&nbsp;

kubectl create -f all-in-one-dbless.yaml

&nbsp;
&nbsp;

### Testing connectivity to Kong Ingress Controller

![screen-shot-kong-no-route](screen-shot/kong-no-route.png)

This is expected since Kong Ingress Controller doesn’t know how to proxy the request yet.

&nbsp;

### Deploy an upstream HTTP application

&nbsp;

kubectl apply -f echo-server.yaml

&nbsp;

### Create routing configuration to proxy /echo requests to the echo server:

&nbsp;

kubectl apply -f echo-ingress.yaml

&nbsp;

### Test the routing rule:

&nbsp;

![screen-shot-kong-route](screen-shot/kong-echo-result.png)

&nbsp;

### Please note that C:\Windows\System32\Drivers\etc\hosts file was updated as below:

&nbsp;

![screen-shot-etc-hosts](screen-shot/etc-hosts.png)

&nbsp;

### Route mapping might be messed up like this:

&nbsp;

![screen-shot-messed-up](screen-shot/messed-up.png)

&nbsp;
