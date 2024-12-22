# Pod

- Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.
- A Pod is a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers.
- Pod will have a one-to-one relationship with containers running your application.
- A single pod can have multiple containers except for the fact that they are usually not multiple containers of the same kind.

Commands for the pod
```
kubectl run nginx --image nginx
kubectl get pods
kubectl create -f redis.yaml
kubectl describe pod <pod name>
kubectl get pods -o wide
```
Iterative commands for pod
```
kubectl run pod <pod-name> --image nginx --dry-run=client -o yaml
kubectl run pod <pod-name> --image nginx --dry-run=client -o yaml > <pod-name>.yaml
```