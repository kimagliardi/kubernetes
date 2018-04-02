# MiniKube setup commands
Remeber: 
- Pod is a instance of a docker container

- Github course repo:
https://github.com/jleetutorial/kubernetes-demo

Commands As Text For Cut & Paste

- Linux: curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
- MacOS: curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/darwin/amd64/kubectl
- Windows: curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.8.0/bin/windows/amd64/kubectl.exe
- chmod +x ./kubectl
- sudo mv ./kubectl /usr/local/bin/kubectl
- kubectl version
- Linux: curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.23.0/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
macOS: curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.23.0/minikube-darwin-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
minikube start
kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.4 --port=8080
kubectl expose deployment hello-minikube  --type=NodePort
kubectl get pod
curl $(minikube service hello-minikube --url)
kubectl delete deployment hello-minikube
minikube stop
---

# Your first K8s app

 Simply deployment of TomCat application


- "Deployments" are the central metaphor for what we'd consider "apps" or "services";
- Deployments are described as a collection of resourcers and references;
- Deployments take many forms based on the type of services being deployed;
- Typically described in **YAML** format.



- We'll deploy the Tomcat App Server using the official docker image
- Key Tasks:
    - Define the deployment
    - Expose the services
    - Deploy it to our cluster.


<center>YAML file</center>

```yaml
apiVersion: apps/v1beta2
kind: Deployment
metadata:
  name: tomcat-deployment
spec:
  selector:
    matchLabels:
      app: tomcat
  replicas: 1
  template:
    metadata:
      labels:
        app: tomcat
    spec:
      containers:
      - name: tomcat
        image: tomcat:9.0
        ports:
        - containerPort: 8080
        
```

- Expose the pod to the external world as a service
```bash
kubectl apply -f ./deployment.yaml

kubectl expose deployment tomcat-deployment --type=NodePort

#Provide us a URL including the port number that we can access are given exposed service
minikube service tomcat-deployment --url
```


### Basic Kubectl

- Provides access to nearly every k8s
- Primary command line access tool

### Cheatsheet
```bash
# List all pods  in all namespaces
# Provides the pod name, how many instances of the pod are running & ready, status, how many times they have restarted, and their age
kubectl get pods


kubectl describe pod <pod name>
---

kubectl expose <type name> <identifier/name> [—port=external port] [—target-port=container-port [—type=service-type]

kubectl port-forward <pod name> [LOCAL_PORT:]REMOTE_PORT]

kubectl attach <pod name> -c <container>

kubectl exec  [-it] <pod name> [-c CONTAINER] — COMMAND [args…]

kubectl label [—overwrite] <type> KEY_1=VAL_1 ….

kubectl run <name> —image=image

```