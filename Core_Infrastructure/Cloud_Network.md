# The Google Cloud Network

## Goals / Purpose

- Designed to `give customers the highest possible throughput` (débit) and `lowest possible latencies for their applications` by **leveraging more than 100 content caching nodes worldwide.**

## Location

- These are locations where high demand content is cached for quicker access, allowing applications to respond to user requests from the location that will provide the quickest response time.
- From redundant cloud regions to high-bandwidth connectivity via subsea cables, every aspect of our infrastructure is designed to deliver your services to your users, no matter where they are around the world.

### Choosing where to locate application affect

- Availability
- Durability
- Latency : measures the time a packet of information takes to travel from its source to its destination

### Google Cloud’s infrastructure

Based in 5 five major geographic locations :

- North America
- South America
- Europe
- Asia
- Australia

### Location division : *Divided into several different regions and zones*

- **What is a region?** :
    - represent independent geographic areas and are composed of zones
    - Example : London, or europe-west2, is a region that currently comprises three different zones.

- **What is a zone?** :
    - Area where Google Cloud resources are deployed.
    - Example : if you launch a virtual machine using Compute Engine, it will run in the zone that you specify to ensure resource redundancy.

- **NB:**
    - You can also run resources in different regions. 
        - Example :  Cloud Spanner multi-region configurations allow you to replicate the database's data not just in multiple zones, but in multiple zones across multiple regions, as defined by the instance configuration.
    - Google Cloud currently supports 118 zones in 39 regions, although this number is increasing all the time.
    - > You can find the most up-to-date numbers at cloud : `google.com/about/locations`

