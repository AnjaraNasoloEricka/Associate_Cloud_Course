# Google Kubernetes Engine 

## How it works ?
- The master controls the cluster 
- The worker nodes run pods 
- A pod holds a set of container 
- Pods are bin-packed as efficiently as configuration and hardware allows
- Controllers provide safeguards so that pods run according to specification (reconciliation loops)
- All components can be deployed in high-availability mode and spread across zones or data centers

## Features 
- Automated deployment and replication of containers
- Online scale-­in and scale-­out of container clusters
- Load balancing over groups of containers
- Rolling upgrades of application containers
- Resiliency, with automated rescheduling of failed containers (i.e., self­-healing of - container instances)
- Controlled exposure of network ports to systems outside of the cluster

## How does GKE make scaling easy?
GKE automatically scales the number of pods and nodes based on the resource consumption of services :
- Vertical Pod Autoscaler (VPA) watches resource utilization of your deployments and adjusts requested CPU and RAM to stabilize the workloads 
- Node Auto Provisioning optimizes cluster resources with an enhanced version of Cluster Autoscaling.