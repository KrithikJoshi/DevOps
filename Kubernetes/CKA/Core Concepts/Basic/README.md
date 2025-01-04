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
- ctr:Used for debugging. Not much of useful.
- nerdctl:Similar to docker commands. Useful when containerd is installed.
- crictl: This command is built by K8 so that we can manage and view the status of the container through controlplane. We can create container with this command but as we run this command in K8 the container will be created inside the K8. As the kubelet is anaware of new container it will remove the same. So this command is useful for viewing the status of the container and logs of the same. Crictl has some new features which docker isn't aware of that crictl is aware of pods. 


ctr image pull command:-
```
ctr images pull docker.io/library/redis:alpine
```

nerdctl run command(similar to docker, just replace docker with nerdctl):-
```
nerdctl run --name redis redis:alpine
```
crictl commands:
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

Documentation steps for Backing up ETCD cluster:
- https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#backing-up-an-etcd-cluster
  

