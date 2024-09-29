# Cloud NAT (Network Adress Translation)

## How is Cloud NAT different from typical NAT proxies ?

- Cloud NAT is a distributed, software-defined managed service, not based on proxy VMs or appliances. This proxyless architecture means higher scalability (no single choke point) and lower latency.
- It also provides destination network address translation (DNAT) for established inbound response packets only.

## Benefits of using Cloud NAT

-**Security** : Helps you reduce the need for individual VMs to each have external IP addresses
-**Availability** : You configure a NAT Gateaway on a Cloud Router which provides the control plane for NAT, holding configuration parameters that you specify
-**Scalability** : Cloud NAT can be configured into automatically scale the number of NAT IP addresses that it uses, and it supports VMs that belong to managed instance groups, including those with autoscaling enabled
-**Performance** : Cloud NAT does not reduce network bandwidth per VM because it is implemented by Google's Andromeda software-defined networking.

> Note : It is a best practice to limit the number of public IP addresses in your network. Cloud NAT (network address translation) lets certain resources without external IP addresses create outbound connections to the internet

## NAT Rules

- create access rules that define how Cloud NAT is used to connect to the internet
- support source NAT based on destination address

> Note :  When you configure a NAT gateway without NAT rules, the VMs using that NAT gateway use the same set of NAT IP addresses to reach all internet addresses