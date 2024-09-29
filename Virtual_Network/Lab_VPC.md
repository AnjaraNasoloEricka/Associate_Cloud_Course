# Lab about VPC Networking

## Objective 
- Explore the default VPC network
- Create an auto mode network with firewall rules
- Convert an auto mode network to a custom mode network
- Create custom mode VPC networks with firewall rules
- Create VM instances using Compute Engine
- Explore the connectivity for VM instances across VPC networks

## Explore the default network 

Each Google Cloud project has a default network with `subnets, routes, and firewall rules`. 

### View the subnets
- In the Cloud Console, on the Navigation menu, click VPC network > VPC networks.
- Notice the default network with its subnets.
- Each subnet is associated with a Google Cloud region and a private `RFC 1918 CIDR block` for its internal IP addresses range and a gateway.

### View the routes
Routes tell VM instances and the VPC network `how to send traffic from an instance to a destination, either inside the network or outside Google Cloud`.

- In the left pane, click `Routes`. Notice that there is a route for each subnet and one for the Default internet gateway (0.0.0.0/0).

> **Note**: Without a VPC network, there are no routes!

### View the firewall rules
Each VPC network implements a distributed virtual firewall that you can configure. Firewall rules allow you to control which packets are allowed to travel to which destinations. 

- In the left pane, click `Firewall`.
    - Notice that there are 4 Ingress firewall rules for the default network:
        - default-allow-icmp
        - default-allow-rdp
        - default-allow-ssh
        - default-allow-internal

## Create an auto mode network
You have been tasked to create an auto mode network with two VM instances. Auto mode networks are easy to set up and use because they `automatically create subnets in each region`.

### Create an auto mode VPC network with firewall rules
1. On the Navigation menu (Navigation menu icon), click VPC network > VPC networks.
2. Click Create VPC network.
3. For Name, type mynetwork
4. For Subnet creation mode, click Automatic.
    > Auto mode networks create subnets in each region automatically.

5. For Firewall rules, select all available rules.
    These are the same standard firewall rules that the default network had. The `deny-all-ingress and allow-all-egress rules` are also displayed, but you cannot select or disable them because they are implied. These two rules have a lower Priority (higher integers indicate lower priorities) so that `the allow ICMP, custom, RDP, and SSH rules` are considered first.

6. Click Create.

7. When the new network is ready, click mynetwork > Subnets. Note the IP address range for the subnets in Region 1 and Region 2.

> Note: If you ever delete the default network, you can quickly re-create it by creating an auto mode network as you just did.

### Create a VM instance in a region 

Create a VM instance in the Region 1 region. Selecting a region and zone determines the subnet and assigns the internal IP address from the subnet's IP address range.

1. On the Navigation menu (Navigation menu icon), click Compute Engine > VM instances.
2. Click Create Instance.
3. Specify the config, and leave the remaining settings as their defaults
4. Click Create.

> Note: The External IP addresses for both VM instances are ephemeral. If an instance is stopped, any ephemeral external IP addresses assigned to the instance are released back into the general Compute Engine pool and become available for use by other projects.

### Verify connectivity for the VM instances
1. On the Navigation menu, click Compute Engine > VM instances.
2. For mynet-us-vm, click SSH to launch a terminal and connect
    > Note: You can SSH because of the allow-ssh firewall rule, `which allows incoming traffic from anywhere (0.0.0.0/0) for tcp:22`. The SSH connection works seamlessly because Compute Engine generates an SSH key for you and stores it in one of the following locations
3. To test connectivity to mynet-eu-vm's internal IP, run the following command, replacing mynet-eu-vm's internal IP : 
    ```bash
    ping -c 3 <Enter mynet-eu-vm's internal IP here>
    ```
> Note : You can ping mynet-eu-vm's internal IP because of the `allow-custom` firewall rule.

4. To test connectivity to mynet-eu-vm's external IP, run the following command, replacing mynet-eu-vm's external IP
    ```bash
        ping -c 3 <Enter mynet-eu-vm's external IP here>
    ```

> Note : You can ping mynet-eu-vm's external IP because of the `mynetwork-allow-icmp` firewall rule.

### Convert the network to a custom mode network

1. On the Navigation menu (Navigation menu icon), click VPC network > VPC networks.
2. Click mynetwork to open the network details.
3. Click Edit.
4. Select Custom for the Subnet creation mode.
5. Click Save.
6. Return to the VPC networks page.
7. Wait for the Mode of mynetwork to change to Custom.

>  Note: Converting an auto mode network to a custom mode network is an easy task, and it provides you with `more flexibility`. We recommend that you `use custom mode networks in production`.

## Create custom mode networks

You have been tasked to create two additional custom networks, `managementnet and privatenet`, along with firewall rules to `allow SSH, ICMP, and RDP ingress traffic and VM instances`

### Create the managementnet network

1. In the Cloud Console, on the Navigation menu (Navigation menu icon), click VPC network > VPC networks.
2. Click Create VPC Network.
3. For Name, type managementnet
4. For Subnet creation mode, click Custom.
5. Specify the following, and leave the remaining settings as their defaults:

| Property    | Value                         |
|-------------|-------------------------------|
| Name        | managementsubnet-us           |
| Region      | Region 1                      |
| IPv4 range  | 10.240.0.0/20                 |

6. Click Done.

7. Click Equivalent Command line.

    These commands illustrate that networks and subnets can be created using the gcloud command line. You will create the `privatenet network` using these commands with similar parameters.

8. Click Close.

9. Click Create.

### Create the privatenet network (using gcloud)

1. In the Cloud Console, click Activate Cloud Shell (Activate Cloud Shell icon).
    - If prompted, click Continue.

2. To create the privatenet network, run the following command. Click Authorize if prompted.
```bash
gcloud compute networks create privatenet --subnet-mode=custom
```

3. To create the privatesubnet-us subnet, run the following command:
```bash
gcloud compute networks subnets create privatesubnet-us --network=privatenet --region=Region 1 --range=172.16.0.0/24
```

4. To create the privatesubnet-eu subnet, run the following command:
```bash
gcloud compute networks subnets create privatesubnet-eu --network=privatenet --region=Region 2 --range=172.20.0.0/20
```

5. To list the available VPC networks, run the following command:
```bash
gcloud compute networks list
```
The output should look like this:

| NAME           | SUBNET_MODE  | BGP_ROUTING_MODE | IPV4_RANGE | GATEWAY_IPV4 |
|----------------|--------------|------------------|------------|--------------|
| managementnet  | CUSTOM       | REGIONAL         |            |              |
| mynetwork      | CUSTOM       | REGIONAL         |            |              |
| privatenet     | CUSTOM       | REGIONAL         |            |              |


6. To list the available VPC subnets (sorted by VPC network), run the following command:
```bash
gcloud compute networks subnets list --sort-by=NETWORK
```

> Note: The managementnet and privatenet networks only have the subnets that you created because they are custom mode networks. mynetwork is also a custom mode network, but it started out as an auto mode network, resulting in subnets in each region.

7. In the Cloud Console, on the Navigation menu (Navigation menu icon), click VPC network > VPC networks.
Verify that the same networks and subnets are listed in the Cloud Console.

### Create the firewall rules for managementnet

1. In the Cloud Console, on the Navigation menu, click **VPC network > Firewall**.
2. Click **Create Firewall Rule**.
3. Specify the following, and leave the remaining settings as their defaults:

   | Property               | Value                                      |
   |------------------------|--------------------------------------------|
   | Name                   | managementnet-allow-icmp-ssh-rdp           |
   | Network                | managementnet                              |
   | Targets                | All instances in the network               |
   | Source filter          | IPv4 Ranges                                |
   | Source IPv4 ranges     | 0.0.0.0/0                                  |
   | Protocols and ports    | Specified protocols and ports              |

   > Note: Make sure to include the `/0` in the Source IPv4 ranges to specify all networks.
   
   - Select **tcp** and specify ports **22** and **3389**.
   - Select **Other protocols** and specify **icmp** protocol.

4. Click **Equivalent Command line**.

   These commands illustrate that firewall rules can also be created using the `gcloud` command line. You will create the privatenet's firewall rules using these commands with similar parameters.

5. Click **Close**.
6. Click **Create**.

### Create the firewall rules for privatenet

1. Return to `Cloud Shell`. If necessary, click Activate Cloud Shell (Activate Cloud Shell icon).

2. To create the privatenet-allow-icmp-ssh-rdp firewall rule, run the following command:
```bash
gcloud compute firewall-rules create privatenet-allow-icmp-ssh-rdp --direction=INGRESS --priority=1000 --network=privatenet --action=ALLOW --rules=icmp,tcp:22,tcp:3389 --source-ranges=0.0.0.0/0
```

The output should look like this:

| NAME                           | NETWORK    | DIRECTION | PRIORITY | ALLOW                | DENY |
|--------------------------------|------------|-----------|----------|----------------------|------|
| privatenet-allow-icmp-ssh-rdp  | privatenet | INGRESS   | 1000     | icmp, tcp:22, tcp:3389 |      |


3. To list all the firewall rules (sorted by VPC network), run the following command:
```bash
gcloud compute firewall-rules list --sort-by=NETWORK
```

The output should look like this:

| NAME                              | NETWORK       | DIRECTION | PRIORITY | ALLOW                        |
|-----------------------------------|---------------|-----------|----------|------------------------------|
| managementnet-allow-icmp-ssh-rdp  | managementnet | INGRESS   | 1000     | icmp, tcp:22, tcp:3389       |
| mynetwork-allow-icmp              | mynetwork     | INGRESS   | 1000     | icmp                         |
| mynetwork-allow-custom            | mynetwork     | INGRESS   | 65534    | all                          |
| mynetwork-allow-rdp               | mynetwork     | INGRESS   | 1000     | tcp:3389                     |
| mynetwork-allow-ssh               | mynetwork     | INGRESS   | 1000     | tcp:22                       |
| privatenet-allow-icmp-ssh-rdp     | privatenet    | INGRESS   | 1000     | icmp, tcp:22, tcp:3389       |


### Create the managementnet-us-vm instance

1. In the Cloud Console, on the Navigation menu (Navigation menu icon), click Compute Engine > VM instances.

2. Click Create instance.

3. Specify the config, and leave the remaining settings as their defaults.

4. Click Advanced options.

5. Click Networking.

6. For Network interfaces, click the dropdown arrow to edit.

7. Specify the following, and leave the remaining settings as their defaults:

| Property   | Value                 |
|------------|-----------------------|
| Network    | managementnet         |
| Subnetwork | managementsubnet-us   |

### Create the privatenet-us-vm instance
1. Return to Cloud Shell. If necessary, click Activate Cloud Shell (Activate Cloud Shell icon).

2. To create the privatenet-us-vm instance, run the following command:

```bash
gcloud compute instances create privatenet-us-vm --zone=Zone 1 --machine-type=e2-micro --subnet=privatesubnet-us --image-family=debian-12 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=privatenet-us-vm
```

3. To list all the VM instances (sorted by zone), run the following command:
```bash
gcloud compute instances list --sort-by=ZONE
```

## Explore the connectivity across networks

> Note: You can ping the external IP address of all VM instances, even though they are in either a different zone or VPC network. This confirms that public access to those instances is only controlled by the ICMP firewall rules that you established earlier. So only mynetwork VPC can ping mynetwork VPC internal IP adress
