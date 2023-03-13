# Kubernetes K8


## Kubernetes set up

First things first, we will need to have docker desktop running.

We can open GitBash terminal as ADMIN and type `kubectl get service` our output should be something like this:

```Linux
$ kubectl get service
Unable to connect to the server: dial tcp [::1]:8080: connectex: No connection could be made because the target machine actively refused it.
```

To resolve this we need to open our Docker Desktop and go to settings. From there we click on "Kubernetes" and Enable Kubernetes. 

![](pictures/Screenshot%202023-03-13%20103329.png)

Lastly we need to click on "Apply& restart". This might take a while so please be patient. Once that is done, you might have to restart your machine. 

This is if the Kubernetes and Docker are running correctly we can see that on the bottom-left corner of Docker Desktop.

![](pictures/running.png)

**NOTE**

To list out useful commands type `kubectl` in GitBash Terminal:

```
kubectl controls the Kubernetes cluster manager.

Find more information at: https://kubernetes.io/docs/reference/kubectl/

Basic Commands (Beginner):
 create          Create a resource from a file or from stdin
 expose          Take a replication controller, service, deployment or pod and expose it as a new Kubernetes service
 run             Run a particular image on the cluster
 set             Set specific features on objects

Basic Commands (Intermediate):
 explain         Get documentation for a resource
 get             Display one or many resources
 edit            Edit a resource on the server
 delete          Delete resources by file names, stdin, resources and names, or by resources and label selector

Deploy Commands:
 rollout         Manage the rollout of a resource
 scale           Set a new size for a deployment, replica set, or replication controller
 autoscale       Auto-scale a deployment, replica set, stateful set, or replication controller

Cluster Management Commands:
 certificate     Modify certificate resources.
 cluster-info    Display cluster information
 top             Display resource (CPU/memory) usage
 cordon          Mark node as unschedulable
 uncordon        Mark node as schedulable
 drain           Drain node in preparation for maintenance
 taint           Update the taints on one or more nodes

Troubleshooting and Debugging Commands:
 describe        Show details of a specific resource or group of resources
 logs            Print the logs for a container in a pod
 attach          Attach to a running container
 exec            Execute a command in a container
 port-forward    Forward one or more local ports to a pod
 proxy           Run a proxy to the Kubernetes API server
 cp              Copy files and directories to and from containers
 auth            Inspect authorization
 debug           Create debugging sessions for troubleshooting workloads and nodes

Advanced Commands:
 diff            Diff the live version against a would-be applied version
 apply           Apply a configuration to a resource by file name or stdin
 patch           Update fields of a resource
 replace         Replace a resource by file name or stdin
 wait            Experimental: Wait for a specific condition on one or many resources
 kustomize       Build a kustomization target from a directory or URL.

Settings Commands:
 label           Update the labels on a resource
 annotate        Update the annotations on a resource
 completion      Output shell completion code for the specified shell (bash, zsh, fish, or powershell)

Other Commands:
 alpha           Commands for features in alpha
 api-resources   Print the supported API resources on the server
 api-versions    Print the supported API versions on the server, in the form of "group/version"
 config          Modify kubeconfig files
 plugin          Provides utilities for interacting with plugins
 version         Print the client and server version information

Usage:
 kubectl [flags] [options]

Use "kubectl <command> --help" for more information about a given command.
Use "kubectl options" for a list of global command-line options (applies to all commands).

# To see all the services running in a cluset, run the following:

kubectl get svc

# The output will have the following format:
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
```



---

## What is Kubernetes K8 ?

Kubernetes is an open-source container orchestration platform that automates the
deployment, scaling, and management of containerized applications.

It allows developers to define how their application should run and it takes care of scheduling containers across a cluster of machines, ensuring that the containers are running and healthy, and scaling the application up or down as demand changes. 

## What are the benefits of K8?

1. Scalability: Kubernetes provides a scalable platform for deploying and managing containerized applications. It can automatically scale applications up or down based on demand, ensuring that the application is always available and responsive.

2. Flexibility: Kubernetes supports multiple container runtimes and can be deployed on a variety of infrastructure, including on-premises servers, public cloud, or hybrid environments.

3. Automation: Kubernetes automates the deployment, scaling, and management of containerized applications, reducing the need for manual intervention and increasing efficiency.

4. Community: Kubernetes has a large and active community of developers, users, and contributors, providing a wealth of resources, documentation, and support.

5. Resilience: Kubernetes provides self-healing capabilities that automatically recover from failures and ensure that applications are always available and responsive.


---

## K8 objects

Kubernetes uses objects to manage applications. The most commonly used objects include **Pod, Deployment, Service, ConfigMap, Secret, and Namespace**. 

These objects are defined using YAML or JSON manifests, which describes the desired state of the object, and Kubernetes uses these manifests to create, update, and delete objects in the cluster as necessary. 

---

## Kubernetes Architecture

![](pictures/Screenshot%202023-03-13%20100411.png)

Kubernetes architecture consists of a ***master node and worker nodes.** 

The master node is responsible for managing the Kubernetes cluster and it's components, including the API server, etcd data store, scheduler, and controller manager. 
The **API server** serves as the front-end for the Kubernetes control plane, allowing users and administrators to interact with the cluster. The **etcd data store** stores configuration data for the cluster. The **scheduler** is responsible for scheduling workloads on the worker nodes, and the **controller manager** manages the state of the cluster by monitoring and reconciling the actual state with the desired state.

The worker nodes are responsible for running applications and workloads, represented by Pods. Each worker node runs a container runtime, such as Docker, and a kubelet agent that communicates with the master node to receive instructions on scheduling and managing Pods. 

Communication between the master and worker nodes is achieved using the Kubernetes API, and communication between the Pods is achieved using a networking plugin, such as Calico or Flannel, which provides an overlay network across the cluster.

## Single-node cluster & multi-node cluster

**1. A single-node** is typically used for development and testing purposes, as it provides an easy and lightweight way to run and test Kubernetes workloads on a local machine. A single-node cluster includes all the components of a standard Kubernetes cluster, including the API server, etcd, kubelet, and kube-proxy, but they all run on a single host.

**2. A multi-node cluster** is used in production environments, where high availability and scalability are important. A multi-node cluster consists of **multiple nodes**, each running the Kubernetes components and hosting one or more Kubernetes workloads.
The nodes communicate with each other to maintain cluster state and ensure that workloads are scheduled and run correctly. 

### Sumarry

In summary, a single-node cluster is useful for testing and development, while a multi-node cluster is necessary for production workloads that require scalability, high availability, and fault tolerance.
---

## K8 Dependencies

There are several dependencies that must be installed on the host system to run a K8s cluster.

1. Container runtime: Kubernetes requires a container runtime, such as Docker

2. etcd: is a distributed key-value store used by Kubernetes to store it's data, including information about the cluster, nodes, pods, and services.

3. kubelet: kubelet is the primary node agent that runs on each worker node in a K8s cluster. It communicates with the control plane to ensure that the containers are running as expected. 

4. kubectl: kubectl is the command-line tool used to interact with a K8s cluster. It can be used to deploy and manage applications, view cluster status and logs, and perform other administrative tasks. 

5. Container Network Interface (CNI): Is a specification for network plugins used by K8s to connect containers within a pod and across different nodes in the cluster. 

**NOTE**

It's important to ensure that all the dependencies are compatible with each other and with the K8s version you are using. It's also recommended to follow the best practices for installing and configuring these dependencies to ensure a secure and stable K8s cluster.

--- 



