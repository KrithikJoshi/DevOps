# Kubernetes Cluster Architecture
- Kube Api Server
- Kube Controller Manager
- ETCD Cluster
- Kube Scheduler
- Kubelet
- Kube Proxy

# ContainerD
ContainerD is the tool similar to docker which is compatible with CRI(Container Runtime Interface) and follows OCI(Open Container Initiative) which consists of standards of image spec and runtime spec.
3 Important types of commands:
- **`ctr`**:Used for debugging. Not much of useful.
- **`nerdctl`**:Similar to docker commands. Useful when containerd is installed.
- **`crictl`**: This command is built by K8 so that we can manage and view the status of the container through controlplane. We can create container with this command but as we run this command in K8 the container will be created inside the K8. As the kubelet is anaware of new container it will remove the same. So this command is useful for viewing the status of the container and logs of the same. Crictl has some new features which docker isn't aware of that crictl is aware of pods. 


**`ctr`** image pull command:-
```
ctr images pull docker.io/library/redis:alpine
```

**`nerdctl`** run command(similar to docker, just replace docker with nerdctl):-
```
nerdctl run --name redis redis:alpine
```
**`crictl`** commands:
```
crictl ps -a
crictl exec -i -t <image name> ls
crictl logs <image name>
crictl pods
crictl images
```
# ETCD:
 - ETCD is a distributed reliable key-value store that is simple, secure & Fast.
 - The ETCD Datastore stores information regarding the cluster such as Nodes, PODS, Configs, Secrets, Accounts, Roles, Bindings and Others.
 - Every information retrieved through **`kubectl get`** is retrieved from etcd cluster.

Important in ETCD Cluster is ETCD Backup. 
This is etcdctl command to set the etcdctl_api to save the snapshot.
```
ETCDCTL_API=3 etcdctl --cert=/etc/kubernetes/pki/etcd/server.crt --key=/etc/kubernetes/pki/etcd/server.key --cacert=/etc/kubernetes/pki/etcd/ca.crt get / --prefix --keys-only
```
Documentation steps for Backing up ETCD cluster:
- https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#backing-up-an-etcd-cluster

# Kube-apiserver

Kube-apiserver is responsible for `authenticating`, `validating requests`, `retrieving` and `Updating data` in ETCD key-value store. In fact kube-apiserver is the only component that interacts directly to the etcd datastore. The other components such as `kube-scheduler`, `kube-controller-manager` and `kubelet` uses the API-Server to update in the cluster in their respective areas.

Commands that describe the kube-apiserver:
```
kubectl get pods -n kube-system kube-apiserver
```
Description of the kube-apiserver pod:
```
kubectl describe pod -n kube-system kube-apiserver
```
Location of manifest file of kube-apiserver:
```
cat /etc/kubernetes/manifests/kube-apiserver.yaml
```
Check the kube-apiserver process
```
ps-aux | grep kube-apiserver
```
# Kube Controller Manager

In kubernetes terms, a controller is a process that continuously monitors the state of the components within the system and works towards bringing the whole system to the desired functioning state.

Types of Controller:-
- `Node Controller` :- Monitors the nodes and takes the necessary action.
- `Replication Controller`:- monitoring the status of replicasets and ensuring that the desired number of pods are available at all time within the set.
- `ReplicaSet`
- `Deployment Controller`
- `Namespace Controller`
- `Replication Controller`
- `Cron Job`
- `Service Account Controller`

Command to view kube-controller-manager
```
kubectl get pod -n kube-system kube-controller-manager
```

Describe the kube-controller-manager
```
kubectl describe pod -n kube-system kube-controller-manager
```

Manifest file of kube-controller-manager
```
cat /etc/kubernetes/manifests/kube-controller-manager.yaml
```
Inspect kube-controller-manager service manually

```
cat /etc/systemd/system/kube-controller-manager.service
```
Check the service running

```
ps -aux | grep kube-controller-manager
```


