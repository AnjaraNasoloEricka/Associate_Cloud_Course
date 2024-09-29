# Cloud Interconnect and Peering

## Layers

- Layer 2 : connections use a VLAN that pipes directly into your GCP environment, providing connectivity to internal IP addresses in the RFC 1918 address space.

- Layer 3 : connections provide access to Google Workspace services, YouTube, and Google Cloud APIs using public IP addresses.

## Services

1. Dedicated : provide a direct connection to Google’s network
    - Direct Peering (supports Layer 3) 
    - Dedicated Interconnect (supports Layer 2)

2. Shared : provide a connection to Google’s network through a partner
    - Carrier Peering (supports Layer 3)
    - Partner interconnect (supports Layer 2 and 3)

> Note : we have also `Cloud VPN` whicThis service uses the public internet because this service uses the public internet, but traffic is encrypted and provides access to internal IP addresses.

### 1. Dedicated Interconnect

#### Feature
- Enables you to transfer large amounts of data between networks, which can be more cost-effective than purchasing additional bandwidth over the public internet.

- Capacity : *10 Gbps* or *100 Gbps* per link


#### How ?

You need to provision a cross connect between the Google network and your own router in a common colocation facility, as shown in this diagram. To exchange routes between the networks, you configure a BGP session over the interconnect between the Cloud Router and the on-premises router.

> Note : only specific location can do that and that's why there are `Partner Interconnect`

### 2. Partner Interconnect

- Provides connectivity between your on-premises network and your VPC network through a supported service provider.

- Capacity : *50 Mbps* or *50 Gps* per connection

### 3. Cross-cloud Interconnect

- Helps you to establish high-bandwidth dedicated connectivity between Google Cloud and another cloud service provider.

- When you buy Cross-Cloud Interconnect, Google provisions a dedicated physical connection between the Google network and that of another cloud service provider.

- Connections are available in two sizes: *10 Gbps* or *100 Gbps*.

### 4. Direct Peering

- Done by exchanging BGP routes between Google and the peering entity.
- You can use it to reach all the Google services, including the full suite of Google Cloud platform products.
- 10 Gps per link

### 5. Carrier Peering

- If you require access to Google public infrastructure and cannot satisfy Goggle's peering requirements, you can connect via a carrier peering partner.
- Work directly with your service provider to get the connection you need and to understand the partner's requirements.
- Varies based on partner offering

### 5. Carrier Peering