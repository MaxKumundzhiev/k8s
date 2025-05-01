- k8s is containes orchestration tool
- features
    - high availability with no downtime
    - scalability
    - disaster recovery (backup and restore)

## philosophy
- k8s is replicating everything, where configurations are defined in deployment component

## components
**pod**
- pod is the samllest k8s component and its an abstraction on top of container - usually 1 application per pod

**node**
- node is a component, which stands for a server (or a worker), where multiple pods components can run
- there 2 types of node
    - master
    - slave

- there 4 processes which has to be installed on a `master` node
    - api server - cluster gateway to interact with cluster + keeps auth sstuff
    - scheduler - just decided on which worker node new pod should be scheduled - scheduler sends request to woker node kubelet
    - controller manager - detect state changes, e.g. of pods
    - etcd - key:value store of a cluster state (every change of a cluster is updated to store)

- there 3 processes which has to be installed on a `slave` (worker) node
    - (runtime) container runtime - process which actually runs the container
    - (scheduling execution and allocating resource) kubelet - process of k8s itself which schedules and runs containers, which has interface for both pod and node. kubelet starts the pod with a container inside, assigning CPU, RAM and resources
    - (communication) kube-proxy - forwards the requests using service component

**service**
- service is a component which provides permanent (static) IP address, which can be attached to a particular pod and service serves as a load balancer which distributes requests between replica pods
- service component is handy to use for communication between pods - cause when pod dies it makes its independent of its IP address
- the lifecycle of service and pod are not connected
- there are 2 types of service component
    - internal - unavaliable for outside access
    - external - avaliable for outside access

**ingress**
- ingress component stands for providing node address in convinient format and forward income requests to expected service component


**configMap**
- configMap component stands for external configurations and u can connect a configMap to a particular pod component. Data is stored in plain text format. But do not put secure info into configMap - its unsecure. For that purpose k8s provides secret component

**secret**
- secret component used to store secret data. Data is stored in base64 encoded format. 

**volume**
- volume component stands for attaching a physical storage (disk) to a pod component (local or remote)

**deployment**
- deployment component stands for defining how many replicas and how to scale up and down ur pods (abstraction on top of pods component)
- db can not be replicated through deployment - because it has state - but k8s provides another component StatefulSet

**StatefulSet**
- StatefulSet component - stands for statefull applications, e.g. databases


## Q/A
```text
Q: How do pods communicate between each other?
A: Each pod gets its own IP address and they communicate using it. When a pod died and new one is created a new IP address will be issued, however it inconvinient.
```


```text
Q: Which k8s component to use for statefull and stateless applications?
A: For statefull applications like dbs use StatefullSet component and for stateless ones use deployment component.
```