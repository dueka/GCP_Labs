# VPC Networking

# Objectives

# Explore the default VPC network

# Create an auto mode network with firewall rules

# Convert an auto mode network to a custom mode network

# Create custom mode VPC networks with firewall rules

# Create VM instances using Compute Engine

# Explore the connectivity for VM instances across VPC networks

Step 1 : Explore the default network

1. VPC network > VPC networks

2. click Firewall.

3. Select all default network firewall rules.

4. Click Delete.

# Delete the default network

1. Select the default network.

2. Click Delete VPC network.

Step 2. Create an auto mode network

1. click VPC network > VPC networks.

2. Create VPC network.

3. Specify name of network

4. For Subnet creation mode, click Automatic\

5. For Firewall rules, select all available rules.

6. Click Create.

# Create a VM instance in us-central1

1. click Compute Engine > VM instances.

2. Click Create

3. Specify Region and Zone.

# Verify connectivity for the VM instances

1. For mynet-us-vm, click SSH

2. test connectivity to mynet-eu-vm's internal IP

   ping -c 3 <Enter mynet-eu-vm's internal IP here>

# Convert the network to a custom mode network

1. click VPC network > VPC networks.

2. Click mynetwork

3. Click Edit.

4. Select Custom for the Subnet creation mode.

5. Save

Step 3. Create custom mode networks

1. Click VPC network > VPC networks.

2. Click Create VPC Network.

3. For Name, type managementnet

4. Subnet creation mode, click Custom.

5. Specify the name, region and IP address range.

6. Click Done.

# Create the privatenet network

1. click Activate Cloud Shell (Cloud Shell).

2. create the privatenet network,

   gcloud compute networks create privatenet --subnet-mode=custom

3. create the privatesubnet-us subnet

   gcloud compute networks subnets create privatesubnet-us --network=privatenet --region=us-central1 --range=172.16.0.0/24

4. create the privatesubnet-eu subnet

   gcloud compute networks subnets create privatesubnet-eu --network=privatenet --region=europe-west1 --range=172.20.0.0/20

5. list the available VPC networks
   gcloud compute networks list

6. list the available VPC subnets
   gcloud compute networks subnets list --sort-by=NETWORK

# Create the firewall rules for managementnet

1. Using the cloud shell.
   gcloud compute --project=qwiklabs-gcp-02-ec68daea878d firewall-rules create managementnet-allow-icmp-ssh-rdp --direction=INGRESS --priority=1000 --network=managementnet --action=ALLOW --rules=tcp:22,tcp:3389,icmp --source-ranges=0.0.0.0/0

# Create the firewall rules for privatenet

1. Using the cloud shell to create the privatenet-allow-icmp-ssh-rdp

   gcloud compute firewall-rules create privatenet-allow-icmp-ssh-rdp --direction=INGRESS --priority=1000 --network=privatenet --action=ALLOW --rules=icmp,tcp:22,tcp:3389 --source-ranges=0.0.0.0/0

2. list all the firewall rules (sorted by VPC network)

   gcloud compute firewall-rules list --sort-by=NETWORK

# Create the managementnet-us-vm instance

1. Using the cloud shell, to create managementnet-us-vm

   gcloud beta compute --project=qwiklabs-gcp-02-ec68daea878d instances create managementnet-us-vm --zone=us-central1-c --machine-type=f1-micro --subnet=managementsubnet-us --network-tier=PREMIUM --maintenance-policy=MIGRATE --service-account=648642018053-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --image=debian-10-buster-v20200910 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=managementnet-us-vm --no-shielded-secure-boot --no-shielded-vtpm --no-shielded-integrity-monitoring --reservation-affinity=any

# Create the privatenet-us-vm instance

1. Activate Cloud Shell

   gcloud compute instances create privatenet-us-vm --zone=us-central1-c --machine-type=f1-micro --subnet=privatesubnet-us --image-family=debian-10 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=privatenet-us-vm

2. list all the VM instances (sorted by zone)

   gcloud compute instances list --sort-by=ZONE
