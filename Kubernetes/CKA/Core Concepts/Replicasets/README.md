# Replicaset
- Before understanding replicaset, older version of replicaset of that is replication must be understood first.

## Replication Controller
- `ReplicationController` ensures that a specified number of pod replicas are running at any one time.
- `ReplicationController` makes sure that a pod or a homogeneous set of pods is always up and available.

Commands of Replication Controller
```
kubectl create -f rc-definition.yaml
kubectl get replicationcontroller <rs-name>
kubectl get pods
kubectl delete replicacontroller/rc <rc-name>
```
## Replicaset

- A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time.
- Usually, you define a Deployment and let that Deployment manage ReplicaSets automatically.
- It's the upgraded version of `Replication Controller`
- In replicaset yaml file we can specify `labels` and `selector` and apply `replicaset` for specific pods instead of applying replicaset to all the pods present in the k8.

Commands of Replicaset
```
kubectl create -f rs.yaml
kubectl get replicaset/rs
kubectl get pods
kubectl delete replicaset/rs <rs-name>
```
Scaling the replicaset 
- This can be scaled in 2 methods.
  - Update the replicaset definition file.
  - Second way is to use the command.

Commands for scaling replicaset
```
kubectl scale replicaset <rs-name> --replicas=6
kubectl scale --replicas=6 -f replicaset-definition.yaml
```
