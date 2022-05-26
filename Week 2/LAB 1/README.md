# Lab 1: Create a Linux virtual machine with the AWS CLI


1. Launch AWS Cloud Shell
I lauched AWS Cloud Shell on the navigation tap

2. Create virtual machine
To create a virtual machine I follwed the following process
> Got a vpc id
 
> Got a keypair

> Got the machine AMI

To create the virtual machine i used the code input

aws ec2 run-instances 
--image-id ami-0022f774911c1d690 
--count 1 
--instance-type t2.micro 
--key-name Jesmykel 
--security-group-ids sg-0fcd61ad8f59f4e2c
 
3. Open port 80 for web traffic
To open port 80 I used the code input

aws ec2 authorize-security-group-ingress 
--group-id sg-0fcd61ad8f59f4e2c 
--protocol tcp 
--port 80 
--cidr 0.0.0.0/0

4. Connect to virtual machine
Before i connect to a virtual machine, I open port 22 using the code input

aws ec2 authorize-security-group-ingress 
--group-id sg-0fcd61ad8f59f4e2c 
--protocol tcp 
--port 22 
--cidr 0.0.0.0/0

Then after which i went to back to the management console to connect the instance using the EC2 instance connect

5. Install web server
To install web server I used the code input

sudo yum update
sudo yum install httpd
sudo systemctl start httpd

6. View the web server in action
I then viewed the webpage in action

Below is a screenshot of the webpage




Notes:
Quickstart: Create a Linux VM

https://aws.amazon.com/getting-started/launch-a-virtual-machine-B-0/
Quickstart for AWS CloudShell

https://docs.aws.amazon.com/cloudshell/latest/userguide/working-with-cloudshell.html