# Google Cloud Migration

Course link : https://cloud.google.com/blog/topics/developers-practitioners/google-cloud-migration-made-easy?hl=en

## Should you migrate to Google Cloud ?
Begin asking yourself those following questions :

1. Are the components of my application stack are virtualized or virtualizable ? 
2. Can my application stack run in a cloud environment while still supporting any and all licensing, security, privacy, and compliance requirements?
3. Can all application dependencies (e.g. 3rd party languages, frameworks, libraries, etc.) be supported in the cloud?

## Which migration path is right for you ?
- Google Cloud managed services
- Containers on GKE or Anthos
- Google Cloud Baremetal solutions
- VMs ("Lift and shift") on Google Compute Engine
- Google Cloud VMWare Engine

## Common use case
### Hybrid Cloud Burst 
- **Cloud interconnect :** set up the connectivity between on-premise and the cloud
- Create a cloud landing zone, this includes creating the project and the resources such as `Google Compute Engine (GCE), Google Kubernetes Engine (GKE), Google Cloud VMware Engine (GCVE) or Anthos`.
- Then lift and shift or lift and optimize from on-premise to cloud in the appropriate resource. 
- At this point you are ready to send the traffic bursts or excess traffic to Google Cloud to lower the stress on the existing data center.

### Modernize with Anthos 
- Setup connectivity with **Cloud interconnect**
- Create a cloud landing zone
- Lift & shift on-premise workloads 
- Build Anthos on-premise landing zone 
- Then, modernize Apps both on-prem and in the cloud.

### Land, expand, retire
- Establish network connectivity to GCP using cloud interconnect
- Create cloud landing zone.
- Then, migrate all workloads.
- Finally, retire Data Center once complete. Iterate through hardware retirement as needed.

### DR Site Promotion 
- Establish network connectivity to GCP using cloud interconnect.
- Create cloud landing zone.
- You are then ready to duplicate all workloads in Cloud.
- Then, swap user connectivity to Cloud as PRIMARY.
- Finally, retire co-lo all at once