# calebpokuackom-syself-devops
Syself // Technical Assessment for Kubernetes DevOps Internship

## Helm Chart to deploy a sample backend
I created a Helm Chart to deploy an example application to a Kubernetes cluster.
In this deployment, I utilized:
- Deployment: Manages replicas of the application
- Service: Defines how to access the pods
- Ingress: Exposes HTTP traffic to external users
- Secrets: Stores sensitive information needed for the application to run
- HPA: Automatically scales the number of pods in the Deployment based on CPU utilization to ensure optimal resource utilization and performance

For database, taking that the application is a stateless application, considering that;
1. I did not provide PersistentVolume and PersistentVolumeClaims for persistent storage
2. I used Deployment instead of StatefulSets.

I would recommend the use of a **Serverless Database**

### Reasons
1. Serverless databases excel in handling stateless workloads.
2. A serverless database can automatically adjust resources in cases of load fluctuations.
3. You only pay for the resources consumed, which is/can be beneficial for initial development and testing.

### Drawbacks
1. For high-performance workloads, a managed or self-managed database might be more suitable.

## Production-grade Kubernetes environment
### Overview
This architecture outlines a self-managed Kubernetes environment based on Ubuntu 24.04 and Kubernetes v1.30.3. It covers both the control plane and worker nodes, emphasizing high availability, scalability, and security.

### Infrastructure Layer
- **Virtual Machines (VMs)**: The underlying hardware. The VMs will host both control plane components and worker nodes.
- **Private Network**: Interconnecting the VMs. This will be isolated from the public internet to enhance security.
- **Storage**: 
  - **Permanent Storage**: A highly-available shared block storage will be used for persistent data volumes.
  - **Ephemeral Storage**: VMs will have local SSD storage for container images and temporary data.
- **Networking**: Illustrating the overlay network for container communication.

### Control Plane
The control plane is responsible for managing the cluster. It consists of etcd, API Server, Controller Manager, Scheduler, and other components deployed across multiple VMs for high availability.
- **Virtual Machines**: Two control plane VMs will be deployed for redundancy.
- **Operating System**: Ubuntu 24.04 will be installed on all control plane VMs.
- **Kubernetes Components**:
  - **etcd**: A strongly consistent, distributed key-value store will be deployed across all control plane VMs to persist the cluster's state.
  - **API Server**: The central point of control for the cluster, handling requests from users and clients.
  - **Controller Manager**: Implements core control loops like replica set, service, endpoint controller.
  - **Scheduler**: Decides which node to place new pods on.
  - **Kubelet**: Runs on each node, communicating with the control plane and managing containers.
  - **Kube-proxy**: Network proxy running on each node, implementing service rules.

### Worker Nodes
The worker nodes provide a running environment for client applications.
- **Virtual Machines**: Multiple worker nodes will be deployed based on workload requirements.
- **Operating System**: Ubuntu 24.04 will be installed on all worker nodes.
- **Container Runtime**: Docker will be used as the container runtime.
- **Kubelet and Kube-proxy**: These components will be installed on each worker node.
- **Node Local Storage**: Each worker node will have local SSD storage for container images and pods.

# TODO
1. Storage
2. Networking
3. Cluster Configuration
4. Security
5. High Availability
6. Monitoring & Logging
7. CI/CD