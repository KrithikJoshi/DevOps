# Deployment

- A Deployment manages a set of Pods to run an application workload.

Deployment definition file
```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: myapp-deployment
      labels:
        app: myapp
        type: front-end
    spec:
     template:
        metadata:
          name: myapp-pod
          labels:
            app: myapp
            type: front-end
        spec:
         containers:
         - name: nginx-container
           image: nginx
     replicas: 3
     selector:
       matchLabels:
        type: front-end
```
Commands for deployment
```
kubectl create -f deployment-definition.yaml
kubectl create deployments <deploy-name> --image nginx --replicas 6 --dry-run=client -o yaml > deployment-definition.yaml
kubectl get deployments
kubectl edit deployment <deploy-name>
```
- Deployment was mainly built over the `replicaset` that is under deployment the monitoring of pods is taken care by the `replicaset` itself.
- Deployment handles the rolling updates as we know that newer version of application emerges so updating of application hosted inside the pods is necessary.
- As there are many pods present for different purposes so we cannot update all the pods at once. So deployment helps to update one pod at a time so that our application can be working fine.

Commands for updating the pods under the deployment
```
kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1
kubectl set image deployment/nginx-deployment *=nginx:1.16.1
```
Here * indicates that all pods in the deployment are updated to image nginx:1.16.1. To update a particular pod use the container name to update the same

Check the history of rolling update
```
kubectl rollout history deployment/nginx-deployment
kubectl rollout history deployment/nginx-deployment --revision=2
```
`--revision=2` this indicates the history of rolling update second time.


Check the status of the rolling update
```
kubectl rollout status deployment/nginx-deployment
```
Undo the rolling update
```
kubectl rollout undo deployment/nginx-deployment
```


