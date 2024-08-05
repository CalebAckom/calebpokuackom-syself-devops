# calebpokuackom-syself-devops
Syself // Technical Assessment for Kubernetes DevOps Internship

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