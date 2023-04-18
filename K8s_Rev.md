.Containers : are best suited to deliver microservices by proividing portable, Isolated VM for Apps

.Why did we go to Container Orchestration ?
>> when make an App (Container) that Consume A ReSRCs Over or Large than ReSrcs that will give : Downtime 
       but Orchestration Solve this Problem : Self healing 

.Container Orchestration : Tool that Managed or automated Cluster like k8s, docker swarm, marathon And Nomad
.Cluster : Group of Nodes (Instances or VMs) 

.Kubernetes : Open SRC System for automating deployment, Scaling and MGM of Containerized Apps
              >> - Writen in Go Lang
              >> - CNCF "Cloud Native Compute Foundation"
.Kubernetes as A Service : Amazon EKS, Google GKE And Azure AKS

.When Existing Updates in Moloithic App : DownTime is a long (Services stop in Client a period of Time)


.Features of K8S :

1- Scalability : Provides Horzintal Scaling / Vertical Scaling of Pods on the basis of CPu Utlization
         pod >>  Smallest deployabe units for Computing    
                 Group of one / more containers that shared storage and network ReSRCs 
         
         -- Horzintal Scaling >>  Adding new pods to improve performance "Replica"    performance بدل ما انت اللي بتظبط ال ريسورسز هو بيضيف نودز علشان يحسن ال  
         -- Vertical Scaling   >>  Modify Attributed ReSRCs of Each node in Your Cluster (Increase / Improve performance of ReSRCs)

2- Self Healing : - autoamticaly replaces and rescheduled Containers from failed nodes. 
                  - it Kills restarts containers unResponsive to health check based on Rules and Policies
                  - it also prevents traffic from being routed to UnResponsive Conatiners

3- Automated Rollouts and Rollbacks : make Rolls out and Rolls back  and Monitoring App's health to prevent any downTime

4- Secret and Configuration Management : Manages Sensitive data and Configuration Management details fo App Separately from Container Image

5- Portability : a Cluster run on any mainstream Linux Distribution, Cloud Provider and new Container RunTime Besides "غير" docker 



Kubernetes Architecture: 

1-Worker nodes : Provide a running envirnment for client Apps These Apps Are Encapaulated in Pods
         >> Componenets of  Worker nodes:
             a- Container Runtime ""pod : through CRI "Container RunTime Interface" 
                 Containerd "docker"                        CRI-O
             b- Node-agent "Kubelet" :  - agent that Running on each node and communicates with Control-plane "Master node" Components 
                                        - Receive pod definations from Api-Server
                                        - Interacts with Container RunTime on nodes to run containers with pods
                                        - Monitor ReSRCs and Health check of pods running Containers
                                                                                -  Connects to Container RunTime through a Plugins based interface > CRI
                           
                          c- Proxy "Kube-proxy" : - Network Agent that runs on each node 
                                     - Responsibe for dynamic Updates and maintenance of All networking rules of node
                                     - F/W Connection Requests to pods
                                     - Responsibe for TCP/UDP AND SCTP F/W  or Round-robin F/W  
             d- Addnons: Cluster Features and Funcationality not yet avalaible in K8S, there for implemented throgh 3rd-party pods and services
                      >>  
                                      
                                - DNS : is a DNS Server required to assign dns records to K8S objects and ReSRCs
                                - Dashboard : web-based UI For Cluster Mgm
                                - Monitoring : Collects Cluster-level Container Metrics and Saves them to Central Data-Store "ETCD"
                                - Logging : Collects Cluster-level Container Logs and Saves them to Central Log-Store for Analysis

2- Master Node "Control-plane": - Provides a Running Environment for Control-plane resposaible for managing the state of K8S Cluster
                                - The Brain "Behind All Operations inside Cluster"
                                - Communicates with K8S Cluster, Users send Requests to Control-plane through "Cli - WebUI - API"
                                - Persist of Cluster state, All Cluster Configurations data is saved to ETCD

          >> Componenets of  Master node:
            
               a- Kube-Api_Server : - Receive Requests that What are you doing?
                                    - Deal with Worker nodes 
                                    - Communicate with ETCD  

               b- Kube Controller Manager "KCM" : - Running and Comparing the Cluster's desired state with Current state
                                                  - Runs Controllers Responsible to act when nodes become unAvaliable to ensure pod counts, to create endpoints
                                                  - Service accounts and API access token  
         
               c- Kube- Scheduler: - assigns pods to nodes
                                   - determines that nodes are valid placement for each pod in Schedulaing Queue According to Constraints and Available ReSRCs     



                              d- Cloud Controller Manager "CCM" : - Link your Cluster into Your Cloud Provider's API 
  
             
               e- ETCD "Data store" : - key value store for most critical data of Distributed System
                                      - Used to persist "يحتفظ"  K8S Cluster state
                                      - Communicate with kube-Api_server 
                         
                              f- Kubectl : - K8S Command line tool allows to run command against K8S Cluster
                            - Deploy Apps, Inspect and manage Cluster ReSRCs and View Logs








# Some Definations:
 1- Pod : one OR More Containers that should be controlled as a single App
 2- Node: - Worker machine in K8S and may be Vm or Phy machine
           - each node is managed by Control-plane "Master"
           - have a multiple of pods 


  3- Control-plane "Master" : handles Scheduling the pods across the nodes in Cluster

 4- Cluster: - Set of nodes that run containerized Apps
             - Allow Containers to run across multiple machines and environments
             - K8S Containers are not restricted "مربوطين" to specific OS  


 5- NameSpaces : way to organize / divded  cluster into Virtual Sub-Clusters

 6- Service : Logical Abstraction for deployed  group of pods in cluster


 7- Deployment: - Tell K8S how to create/ modify instances of pods that hold a containerized App
                - can scale the number of replica pods
                - enable rollout of update code in Controller manager or Rollback to earlier deployment version 


 8- Workloads : App that Running on K8, Single Component that work together

 9- Volume: Applies to a whole pod and is mounted on all containers in pod
 
 10- ReplicaSet: maintain s stable set of Replica pods running at any given time

 11- Ingress : Api object that provides routing rules to manage external user's access to services in K8S Cluster vis HTTP / HTTPS

 12- Minikube : tool that run K8S locally
  





## Commands
 1- kubectl create: Creates a resource from a file or URL 
           $ kubectl create -f <file.yaml>
           $ kubectl create deployment <deployment-name> --image=<image-name>
 
2- kubectl get: Retrieves one or more resources
           $ kubectl get pods
           $ kubectl get deployments
           $ kubectl get services

3- kubectl describe: Describes a resource in detail
           $ kubectl describe pod <pod-name>
           $ kubectl describe deployment <deployment-name>
           $ kubectl describe service <service-name>

   
4- kubectl delete: Deletes a resource  
           $ kubectl delete pod <pod-name>
           $ kubectl delete deployment <deployment-name>
           $ kubectl delete service <service-name>

5- kubectl apply: Applies a configuration to a resource
           $ kubectl apply -f <file.yaml>
           $ kubectl apply -f <directory-name>

6- kubectl logs: Displays logs from a container in a pod

           $ kubectl logs <pod-name> <container-name>

7- kubectl exec: Runs a command in a container in a pod
           $ kubectl exec -it <pod-name> -- <command>

8- kubectl port-forward: Forwards a local port to a port on a pod  
           $ kubectl port-forward <pod-name> <local-port>:<pod-port>

9- kubectl scale: Scales a deployment up or down   
           $ kubectl scale deployment <deployment-name> --replicas=<number-of-replicas>

10- kubectl rollout: Manages rollouts and rollbacks of deployments
           $ kubectl rollout status deployment/<deployment-name>
           $ kubectl rollout history deployment/<deployment-name>
           $ kubectl rollout undo deployment/<deployment-name>
 

11- kubectl apply --dry-run: Checks the validity of a configuration file without actually applying it.
           $ kubectl apply -f <file.yaml> --dry-run

12- kubectl explain: Shows detailed information about a Kubernetes object, including its fields, their types, and any constraints.
           $ kubectl explain <resource-name>

13- kubectl diff: Shows differences between the current state of a resource and the desired state as specified in a configuration file.
           $ kubectl diff -f <file.yaml>

14- kubectl label: Adds or removes labels from a resource.
           $ kubectl label <resource-type> <resource-name> <label-key>=<label-value>
           $ kubectl label <resource-type> <resource-name> <label-key>-

15- kubectl annotate: Adds or removes annotations from a resource.
           $ kubectl annotate <resource-type> <resource-name> <annotation-key>=<annotation-value>
           $ kubectl annotate <resource-type> <resource-name> <annotation-key>-
  
   
16- kubectl patch: Modifies a field of a resource using a JSON or YAML patch.
           $ kubectl patch <resource-type> <resource-name> --patch <patch-file.yaml>

17- kubectl apply --prune: Deletes resources that are not specified in a configuration file.
           $ kubectl apply -f <file.yaml> --prune

18- kubectl top: Shows the resource usage of nodes or pods in a cluster.
           $ kubectl top nodes
           $ kubectl top pods

19- kubectl proxy: Creates a proxy server between the Kubernetes API server and a local machine.
           $ kubectl proxy

20- kubectl debug: Runs a debugging session inside a container in a pod.
           $ kubectl debug <pod-name> -c <container-name>

21- K8s.yaml


a- apiVersion: The version of the Kubernetes API that the object uses. For example, apiVersion: apps/v1 specifies the apps API version.

b- kind: The type of Kubernetes object that the yaml file defines. For example, kind: Deployment defines a Deployment object.

c- metadata: The metadata section includes information about the object, such as its name, labels, and annotations.

d- spec: The spec section includes the desired state of the object, including its configuration and any dependencies it may have.

e- selector: The selector section is used to select the subset of resources to which the configuration should be applied. For example, a selector might select all resources with a specific label.

f- template: The template section is used to define the pod template for the deployment, including any containers, volumes, and other settings.

g- containers: The containers section is used to define the containers to be run in the pod. Each container includes information about its image, environment variables, ports, and other settings

``` yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: nginx:latest
        ports:
        - containerPort: 80

```  
                      
 
     
