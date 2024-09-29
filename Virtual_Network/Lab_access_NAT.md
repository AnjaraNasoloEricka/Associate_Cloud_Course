# Implement Private Google Access and Cloud NAT

## Task 1. Create the VM instance

### Create a VPC network and firewall rules
1. In the Cloud Console, navigate to **VPC network > VPC networks**.
2. Click **Create VPC Network**.
3. Set the following parameters:
   - **Name**: privatenet
   - **Subnet creation mode**: Custom
4. For the new subnet, specify the following:
   - **Name**: privatenet-us
   - **Region**: REGION
   - **IPv4 address range**: 10.130.0.0/20
5. Click **Done** and then **Create**.

6. In the left pane, click **Firewall**.
7. Click **Create Firewall Rule**.
8. Set the following parameters:
   - **Name**: privatenet-allow-ssh
   - **Network**: privatenet
   - **Targets**: All instances in the network
   - **Source filter**: IPv4 ranges
   - **Source IPv4 ranges**: 35.235.240.0/20
   - **Protocols and ports**: For tcp, select and specify port 22.
9. Click **Create**.

### Create the VM instance with no public IP address
1. In the Cloud Console, navigate to **Compute Engine > VM instances**.
2. Click **Create Instance**.
3. Set the following parameters:
   - **Name**: vm-internal
   - **Region**: REGION
   - **Zone**: ZONE
   - **Series**: E2
   - **Machine type**: e2-medium (2vCPU, 1 core, 4 GB memory)
   - **Boot disk**: Debian GNU/Linux 12 (bookworm)
4. Click **Advanced options**.
5. Click **Networking**.
6. In **Network interfaces**, click the default network to edit it.
7. Set the following parameters:
   - **Network**: privatenet
   - **Subnetwork**: privatenet-us
   - **External IPv4 address**: None
8. Click **Done** and then **Create**.
9. Verify that the External IP of vm-internal is None.

### SSH to vm-internal to test the IAP tunnel
1. In the Cloud Console, click **Activate Cloud Shell**.
2. If prompted, click **Continue**.
3. Run the following command to connect to vm-internal:
   gcloud compute ssh vm-internal --zone ZONE --tunnel-through-iap
4. If prompted, click **Authorize**.
5. When prompted, type **Y** to continue.
6. When prompted for a passphrase, press **ENTER** twice.
7. Verify the command prompt changed to `@vm-internal`.
8. Run the following command to test external connectivity:
   ping -c 2 www.google.com
   This should not work as vm-internal has no external IP address.
9. To return to your Cloud Shell instance, run:
   exit

## Task 2. Enable Private Google Access

### Create a Cloud Storage bucket
1. In the Cloud Console, navigate to **Cloud Storage > Buckets**.
2. Click **Create**.
3. Set the following parameters:
   - **Name**: Enter a globally unique name
   - **Location type**: Multi-region
4. Click **Create** and ensure public access prevention is enabled if prompted.
5. Store the name of your bucket in an environment variable:
   export MY_BUCKET=[enter your bucket name here]
6. Verify it with:
   echo $MY_BUCKET

### Copy an image file into your bucket
1. In Cloud Shell, run:
   gcloud storage cp gs://cloud-training/gcpnet/private/access.svg gs://$MY_BUCKET
2. Verify the image was copied by navigating to your bucket in the Cloud Console.

### Access the image from your VM instance
1. In Cloud Shell, run:
   gcloud storage cp gs://$MY_BUCKET/*.svg .
   This should work as Cloud Shell has an external IP address.
2. Connect to vm-internal:
   gcloud compute ssh vm-internal --zone ZONE --tunnel-through-iap
3. Store the name of your bucket in an environment variable:
   export MY_BUCKET=[enter your bucket name here]
4. Verify it with:
   echo $MY_BUCKET
5. Try to copy the image to vm-internal:
   gcloud storage cp gs://$MY_BUCKET/*.svg .
   This should not work as vm-internal can only send traffic within the VPC network.

### Enable Private Google Access
1. In the Cloud Console, navigate to **VPC network > VPC networks**.
2. Click **privatenet** to open the network.
3. Click **Subnets**, then **privatenet-us**.
4. Click **Edit**.
5. For **Private Google access**, select **On**.
6. Click **Save**.

### Verify Private Google Access
1. In Cloud Shell, connect to vm-internal:
   gcloud compute ssh vm-internal --zone ZONE --tunnel-through-iap
2. Try to copy the image to vm-internal:
   gcloud storage cp gs://$MY_BUCKET/*.svg .
   This should work as vm-internal's subnet has Private Google Access enabled.

## Task 3. Configure a Cloud NAT gateway

### Try to update the VM instances
1. In Cloud Shell, run:
   sudo apt-get update
   This should work as Cloud Shell has an external IP address.
2. Connect to vm-internal:
   gcloud compute ssh vm-internal --zone ZONE --tunnel-through-iap
3. Try to update vm-internal:
   sudo apt-get update
   This should only work for Google Cloud packages.

### Configure a Cloud NAT gateway
1. In the Google Cloud Console, search for **Network services** and click **Network services**.
2. Click **Cloud NAT**.
3. Click **Get started** to configure a NAT gateway.
4. Set the following parameters:
   - **Gateway name**: nat-config
   - **Network**: privatenet
   - **Region**: REGION
   - **Cloud Router**: Create new router
   - **Name**: nat-router
5. Click **Create** and wait for the gateway's status to change to **Running**.

### Verify the Cloud NAT gateway
1. Wait for a few minutes to ensure the NAT configuration propagates to the VM.
2. Connect to vm-internal:
   gcloud compute ssh vm-internal --zone ZONE --tunnel-through-iap
3. Try to re-synchronize the package index:
   sudo apt-get update
   This should work as vm-internal is using the NAT gateway.
4. To return to your Cloud Shell instance, run:
   exit

## Task 4. Configure and view logs with Cloud NAT Logging

### Enabling logging
1. In the Google Cloud Console, navigate to **Network services > Cloud NAT**.
2. Click on the **nat-config** gateway and then click **Edit**.
3. Click the **Advanced configurations** dropdown to open that section.
4. Under **Logging**, select **Translation and errors** and then click **Save**.

### Viewing Logs
1. Click on **nat-config** to expose its details. Then click on the **Logs** tab. Click the link to **Logging**.
2. This will open a new tab with **Logs Explorer**. You may need to wait for a few minutes. If you do not see any logs, repeat the steps in the **Generating logs** section.

### Generating logs
1. Connect to vm-internal:
   gcloud compute ssh vm-internal --zone ZONE --tunnel-through-iap
2. Try to re-synchronize the package index of vm-internal by running:
   sudo apt-get update
3. To return to your Cloud Shell instance, run:
   exit

### Viewing Logs
1. Return to your **Logs Explorer** tab, and in the navigation menu, click **Logs Explorer**. You should see two new logs that were generated after connecting to the internal VM.
