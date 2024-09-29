# Cloud VPN

## Types of VPN

- HA VPN
- Classic VPN

### Classic VPN

- Securely connects your on-premises network to your Google Cloud VPC network through an **IPsec VPN tunnel**
- SLA of 99,99 %
- Doesn't support use cases where client computers need to “dial in” to a VPN using client VPN software
- Supports :
    - `Dynamic routes` configured with Cloud Router
    - `Static routes`
    - `IKEv1 and IKEv2 ciphers`

> Note : Traffic traveling between the two networks is **encrypted** by one `VPN gateway`, then **decrypted** by the other `VPN gateway`

#### Cloud VPN Gateway

The Cloud VPN gateway is a regional resource that uses a regional **external IP address**.

#### Topology

Create a connection between :

- two VPN gateways (by external IP address)
- two VPN tunnels

### HA VPN

HA VPN is a high availability Cloud VPN solution that lets you securely connect your on-premises network to your Virtual Private Cloud (VPC) network through an IPsec VPN connection in a single region.

- SLA of 99.99% availability

- Supports :
    -  Site-to-site VPN in one of the following recommended topologies or configuration scenarios:
        - An HA VPN gateway to peer VPN devices An HA VPN
        - An HA VPN gateway to an Amazon Web Services (AWS) virtual private gateway
        - Two HA VPN gateways connected to each other

#### Topology

- Configure :
    - 2 or 4 tunnels from your HA VPN gateway to your peer VPN gateway or to another HA VPN gateway

- Google Cloud automatically chooses two external IP addresses to support `multiple tunnels`

## Dynamic routing with Cloud Router

In order to use dynamic routes, you need to configure Cloud Routers.

Cloud Router can manage routes for a Cloud VPN tunnel using Border Gateway Protocol, or BGP.
This routing method allows for routes to be updated and exchanged without changing the tunnel configuration.

XYAH5OFAFLBM2DE6

MY_BUCKET_NAME_1=qwiklabs-gcp-00-a31ed2596b71
MY_BUCKET_NAME_2=qwiklabs-gcp-00-a31ed2596b70