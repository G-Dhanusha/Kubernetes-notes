## Kubernetes-notes [Referhere](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

## What is Kubernetes(K8s)?
  * Kubernetes is a portable, extensible, open source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation.

## Why you need Kubernetes and what it can do?

 * Containers are a good way to bundle and run your applications. 
 * In a production environment, you need to manage the containers that run the applications and ensure that there is no downtime
 * **Kubernetes provides you with**: 

     `Self-healing` 
   
   (Kubernetes restarts containers that fail, replaces containers, kills containers that don't respond to your user-defined health check, and doesn't advertise them to clients until they are ready to serve.)
    
    `Secret and configuration management` 
    
    (Kubernetes lets you store and manage sensitive information, such as passwords, OAuth tokens, and SSH keys. You can deploy and update secrets and application configuration without rebuilding your container images, and without exposing secrets in your stack configuration.)

   `Horizontal scaling` 
   
   (Scale your application up and down with a simple command, with a UI, or automatically based on CPU usage.)

   `Service discovery and load balancing` 
   
   (Kubernetes can expose a container using the DNS name or using their own IP address)

   `Automated rollouts and rollbacks` 
   
   (You can describe the desired state for your deployed containers using Kubernetes, and it can change the actual state to the desired state at a controlled rate)

   `Automatic bin packing` 
   
   (You provide Kubernetes with a cluster of nodes that it can use to run containerized tasks. You tell Kubernetes how much CPU and memory (RAM) each container needs. Kubernetes can fit containers onto your nodes to make the best use of your resources.)
   
## Core Components 

* A Kubernetes cluster consists of a control plane and one or more worker nodes. 
* Here's a brief overview of the main components:

### Control Plane Components:

1) **`kube-apiserver`** : The core component server that exposes the Kubernetes HTTP API
2) **`etcd`**: Consistent and highly-available key value store for all API server data
3) **`kube-scheduler`**: Looks for Pods not yet bound to a node, and assigns each Pod to a suitable node. 
4) **`kube-controller-manager`**:  Runs controllers to implement Kubernetes API behavior.
5) **`cloud-controller-manager (optional)`** : Integrates with underlying cloud provider(s).

### Node Components 

Run on every node, maintaining running pods and providing the Kubernetes runtime environment:

1) **`kubelet`**: Ensures that Pods are running, including their containers.
2) **`kube-proxy (optional)`**: Maintains network rules on nodes to implement Services.
3) **`Container runtime`**: Kubernetes 1.31 requires that you use a runtime that conforms with the Container Runtime Interface (CRI).
    * how to use several common container runtimes with Kubernetes.
        * containerd
        * CRI-O
        * Docker Engine
        * Mirantis Container Runtime 
        (Mirantis Container Runtime (MCR) is a commercially available container runtime that was formerly known as Docker Enterprise Edition.)
    * Kubernetes releases before v1.24 included a direct integration with Docker Engine, using a component named `dockershim`
    
    * **`cgroup drivers`** :
        * On Linux, control groups are used to constrain resources that are allocated to processes.
        * Both the kubelet and the underlying container runtime need to interface with control groups to enforce `resource management for pods and containers` and set resources such as cpu/memory requests and limits.
        * To interface with control groups, the kubelet and the container runtime need to use a **`cgroup driver`**. 
        * It's critical that the kubelet and the container runtime use the same cgroup driver and are configured the same.
        * There are two cgroup drivers available:
            * cgroupfs
            * systemd
        `cgroupfs`
        The cgroupfs driver is the default cgroup driver in the kubelet.



