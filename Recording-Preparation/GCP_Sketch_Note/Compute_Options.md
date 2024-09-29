# Choosing a Google Cloud compute option

## Services 
- Compute Engine
- Kubernetes Engine 
- Cloud Run 
- App Engine 
- Cloud Functions 

## Use case 
- **Compute Engine :** if you are migrating a legacy application with specific licensing, OS, kernel, or networking requirements. Examples: Windows-based applications, genomics processing, SAP HANA

- **Kubernetes Engine :** if your application needs a specific OS or network protocols beyond HTTP/s. When you use GKE, you are using Kubernetes, which makes it easy to deploy and expand into hybrid and multi-cloud environments

- **Anthos :** is a platform specifically designed for hybrid and multi-cloud deployments. It provides single-pane-of-glass visibility across all clusters from infrastructure through to application performance and topology. Example: Microservices-based applications

- **Cloud Run :** you just need to deploy a containerized application in a programming language of your choice with HTTP/s and websocket support. Examples: `websites, APIs, data processing apps, webhook`

- **App Engine :**  if you want to deploy and host a web based application (HTTP/s) in a serverless platform. Examples: web applications, mobile app backends

- **Cloud Function** : if your code is a function and just performs an action based on an event/trigger from Pub/Sub or Cloud Storage.

## Open source Compute Options 
- GKE
- Cloud Run
- Cloud Functions

## Billing
- Compute Engine and GKE billing models are `based on resources`, which means `you pay for the instances you have provisioned`, independent of usage. You can also take advantage of sustained and committed use discounts. 

- Cloud Run, App Engine, and Cloud Functions are billed `per request,` which means you `pay as you go`. 

