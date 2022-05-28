# Lab 3: Manage Packages and Services on a Linux VM (Azure or AWS)


1. CREATE A LINUX VM

To create a linux VM, i used an exiting keypair, vpc, a linux AMI and security group and i used the input code

aws ec2 run-instances 
--image-id ami-0022f774911c1d690 
--count 1 
--instance-type t2.micro 
--key-name Jesmykel 
--security-group-ids sg-0c76c8a2d3cd4ad3d
--subnet-id subnet-06813ed0fa4467465


2. INSTALL THE APACHE WEB SERVER

To install an Apache web server, I went ahead the launch the instance from the management console using the EC2 instance connect of which i then use the input code

sudo yum update -y
sudo yum install httpd -y

3. START THE SERVICE STATUS VIA COMMAND LINE

To start the service i used the input code 

sudo systemctl start httpd

4. INVESTIGATE THE SERVICE STATUS VIA COMMAND LINE

To investigate the service status i used the code input

systemctl status httpd.service

5. STOP THE SERVICE

To stop service i used the code input

systemctl stop httpd.service


Challenge: Create a boostrapping script that will install and start this service on new EC2 VMs

I created a boostrapping in the maangement console under the "Advance setting; users data" using the code input
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd 

Notes:

Install and Configure Apache (Ubuntu)

https://ubuntu.com/tutorials/install-and-configure-apache#1-overview
How to install Apache on RHEL 8 / CentOS 8 Linux

https://linuxconfig.org/installing-apache-on-linux-redhat-8
How to use cloud-init to customize a Linux virtual machine in Azure on first boot

https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-automate-vm-deployment
Create bootstrap actions to install additional software

https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-bootstrap.html