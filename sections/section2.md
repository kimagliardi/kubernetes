# Kubernetes Architecture

![alt](/images/kubarch.jpg)

- Node is a worker machine in Kubernetes. Can be a VM or a Fisical server;
- Kubernetes consist in any number of nodes.

Some concepts:
- **Kubelet**:
    - "node agent" that runs on each node;
    - It's responsible for what's running on an individual machine, you can think of it as a process watcher like supervisord, but focused on running containers. It has one job: given a set of containers to run, make sure they are all running;
    - Kubelets run **pods**.
- **kube-proxy**:
    - Enables the Kubernetes service abstraction by maintaining network rules on the host and performing connection forwarding. 
---

# Scaling Kubernetes

- Stateful vs Stateless Applications
    - **Stateful applications**: Store data from previous sessions, limiting the data that needs to be stored on the client end and retaining information on the server from one use to the next. This data may store user login information, preferences, variables of web service funcions and more.
    - **Stateless applications**: Is an application program that does not save client data generated in one session for use in the next session with that client. Each sessino is carried out as if it was the first time and responses are note dependent upon data from a previous session.

- **How state is handled can either enable or interfere with scaling, it most certainly dictates how you'll scales**
- Kubernetes support both patterns. But it's a good practice use statless app whenever possible.

![alt](/images/replica.jpg)

- Command to scale a existent deployment without stop time:
```bash
kubectl scale --replicas=4 deployment/tomcat-deployment
```

 - **TIP**: Actions about deployments:
    - kubectl **action** deployments **deploymentName**


![alt](/images/loadbalancer.jpg)

<center> Commands for copy and paste </center>

```bash
kubectl scale —replicas=4 deployment/tomcat-deployment 

kubectl expose deployment tomcat-deployment --type=NodePort

kubectl expose deployment tomcat-deployment —type=LoadBalancer —port=8080 —target-port=8080 —name tomcat-load-balancer

kubectl describe services tomcat-load-balancer

kubectl describe services tomcat-load-balance
```

## Deployments Commands

<center> Commands for copy and paste </center>

```bash
    kubectl get deployments
    kubectl rollout status
    kubectl set image
    kubectl rollout history
```
