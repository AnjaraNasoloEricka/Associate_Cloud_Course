# HTTPS Load Balancing

## Features

- Target HTTPS Proxy
- One signed SSL cerficate installed (mininmum)
- Client SSL session terminates at the load balancer
- Support the QUIC transport layer protocol that allows for faster client connection initiation, eliminates head-of-line blocking in multiplexed streams, and supports connection migration when a client's IP address changes.

## SSL certificates

- Up to 15 SSL certificates (per target proxy)
- For each certificate :
    - Create an SSL certificate resource (used only with the load balancing proxies such as a target HTTPS proxy or target SSL proxy)


## Backend buckets

- Allow you to use Google Cloud Storage buckets with HTTP(S) Load Balancing.
- Example of use case :
    - send requests for dynamic content, such as data, to a backend service; and send requests for static content, such as images, to a backend bucket.

## Network endpoint group (NEG)

- Configuration object that specifies a group of a backend endpoint or services.

- There are 4 types of NEG : 
    - Zonal : contains one or more endpoints that can be Compute Engine VMs or services running on the VMs.
    - Internet : contains a single endpoint that is hosted outside of Google Cloud.
    - Hybrid connectivity : Traffic Director services running outside of Google Cloud.
    - Serverless : Cloud Run, App Engine, Cloud Functions services residing in the same region as the NEG.