# Lab 3: GCP

## Compute Engine

### Tutorials

[Quickstart using a Linux VM](https://cloud.google.com/compute/docs/quickstart-linux "Quickstart using a Linux VM")

[Connect to Linux VMs](https://cloud.google.com/compute/docs/instances/connecting-to-instance "Connect to Linux VMs")

[Connecting to Linux VMs using advanced methods](https://cloud.google.com/compute/docs/instances/connecting-advanced "Connecting to Linux VMs using advanced methods")

[Using startup scripts on Linux VMs](https://cloud.google.com/compute/docs/instances/startup-scripts/linux "Using startup scripts on Linux VMs")

[Querying VM metadata](https://cloud.google.com/compute/docs/metadata/querying-metadata "Querying VM metadata")

## gcloud

### Understanding commands

```bash
# The gcloud command format.
gcloud + release level (optional) + component + entity + operation + positional args + flags
```

```bash
# Example gcloud command for creating a virtual machine instance.
gcloud compute instances create <instance_name> --zone=<zone>
```

## Running commands

```bash
# Get the gcloud help information.
gcloud help
```

```bash
# Get the gcloud cheat sheet.
gcloud cheat-sheet
```

```bash
# Get projects help information.
gcloud projects --help
```

```bash
# Get projects create help information.
gcloud projects create --help
```

Below are the expected processes i went through on the gcp cli plaform;

I used the gcp platform to create an instance using the code input
gcloud projects create jesmykel --name=JesmykelGCP --set-as-default
```

I the code input below to list the billing account available 
gcloud beta billing accounts list
```

I linked the billing account with the code input
gcloud beta billing projects link jesmykel --billing-account=001KR5-7TYD37-7HDEC5
```

I used the code input below to echo service 
SERVICE=$(gcloud services list --available --filter="NAME ~ ^compute" --format="value(NAME)")
echo $SERVICE
```

I used the code input below to enable service
gcloud services enable $SERVICE
```

I used the code input to set region
gcloud config set compute/region europe-east1
```

I used the code input to set zone
gcloud config set compute/zone europe east1 b
```

I used the code input to create a firewall rule
gcloud compute firewall-rules delete default-allow-icmp default-allow-internal default-allow-rdp default-allow-ssh
```

I used the code input to delete the default network
gcloud compute networks delete default
```

I used the code input to create to create a custom mode network
gcloud compute networks create vpc-network --subnet-mode=custom
```

I used the code input to create a subnet
gcloud compute networks subnets create default --network=vpc-network --range=10.0.1.0/24
```

I used the code input to add the external IP from the Cloud Shell session to variable, add CIDR notation, and echo result.
SHELL_EXTERNAL_IP=$(curl ifconfig.co)
SHELL_EXTERNAL_IP="$SHELL_EXTERNAL_IP""/32"
echo $SHELL_EXTERNAL_IP
```

I used the code input to create a firewall rule for SSH traffic.
gcloud compute firewall-rules create allow-ssh-ingress \
  --network=vpc-network \
  --priority=1000 \
  --direction=INGRESS \
  --action=ALLOW \
  --target-tags=ssh \
  --source-ranges=$SHELL_EXTERNAL_IP \
  --rules=tcp:22
```

I used the code input to create a firewall rule for web traffic.
gcloud compute firewall-rules create allow-web-ingress \
  --network=vpc-network\
  --priority=1000 \
  --direction=INGRESS \
  --action=ALLOW \
  --target-tags=web \
  --source-ranges=0.0.0.0/0 \
  --rules=tcp:80,tcp:443 
```

I used the code input to create a service account.
gcloud iam service-accounts create web-instance-01 --display-name=web-instance-01
```

I used the code input to add the email address of the service account to a variable and echo the result.
SERVICE_ACCOUNT=$(gcloud iam service-accounts list --filter="email ~ ^web-instance-01" --format="value(email)")
echo $SERVICE_ACCOUNT
```

I used the code input to create the instance, including a startup script.
gcloud compute instances create web-instance-01 \
  --machine-type=e2-micro \
  --description="Web server" \
  --image-project=ubuntu-os-cloud \
  --image-family=ubuntu-2004-lts \
  --network=vpc-network \
  --subnet=default \
  --service-account=$SERVICE_ACCOUNT \
  --tags=ssh,web \
```

I used the code input to connect to the instance over SSH.
gcloud beta compute ssh web-instance-01
```

I the verified that the Apache HTTP Server service is active (running) using the code input
systemctl status apache2.service
```

I then verified the custom index.html file using the code input
cat /var/www/html/index.html
```

I then exited the SSH connection.
exit
```

I then added the external IP from the instance to a variable, add the HTTP protocol, and echo the result.
HTTP_ADDRESS=$(gcloud compute instances describe web-instance-01 --format="value(networkInterfaces[0].accessConfigs[0].natIP)")
HTTP_ADDRESS="http://""$HTTP_ADDRESS"
echo $HTTP_ADDRESS
```

I Verified if the instance is reachable
curl $HTTP_ADDRESS
```

I then finally stopped the instance
gcloud compute instances stop web-instance-01
```

## More information

[Free Trial and Free Tier](https://cloud.google.com/free "Free Trial and Free Tier")

[Compute Engine documentation](https://cloud.google.com/compute/docs "Compute Engine documentation")

[Cloud Shell documentation](https://cloud.google.com/shell/docs "Cloud Shell documentation")

[Cloud SDK documentation](https://cloud.google.com/sdk/docs "Cloud SDK documentation")

[The gcloud tool overview](https://cloud.google.com/sdk/gcloud "The gcloud tool overview")

[The gcloud cheat sheet](https://cloud.google.com/sdk/docs/cheatsheet "The gcloud cheat sheet")

[The gcloud cheat sheet: Understanding commands](https://cloud.google.com/sdk/docs/cheatsheet#understanding_commands "The gcloud cheat sheet: Understanding commands")
