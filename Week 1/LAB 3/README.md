# Lab 3: Manage Azure disks with the Azure CLI

Task:

1. DEFAULT AZURE DISKS

    To know about Azure disks i visited the link (https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-disks)
2. Azure data disks

    To know about Azure data disks i visited the link(https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-disks)
3. VM DISK TYPES

    To know about VM disk types i visited the link(https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-disks)
4. LAUNCH AZURE CLOUD SHELL

    I launched cloud shell from the navigation pan on azure portal
5. CREATE AND ATTACH DISKS

To create and attach disks, i followed the process bellow

> I created a resource group with a new two data disk sizes of 10gb each using the code input 

az vm create 
--resource-group JesmykelRG1 
--admin-username azureuser 
--image UbuntuLTS 
--name myVM 
--size Standard_B1s 
--generate-ssh-keys 
--data-disk-sizes-gb 10 10

6. PREPARE A DATA DISKS

In order to prepare disks, I undergo the following processes

> Created an ssh connection using the code input

ssh azureuser@20.248.180.206

> Partitioned the disk with "parted" using the code input

sudo parted /dev/sdc --script mklabel gpt mkpart xfspart xfs 0% 100%

I wrote a file system to the partition by using the mkfs command

sudo mkfs.xfs /dev/sdc1

I used partprobe to make the OS aware of the change.

sudo partprobe /dev/sdc1

I then mounted the new disk so that it is accessible in the operating system using the code input

sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive

The disk was now accessed through the /datadrive mountpoint, which was verified by running the df -h command below

df -h | grep -i "sd"

Which gave an output

/dev/sda1        29G  1.5G   28G   5% /
/dev/sda15      105M  4.4M  100M   5% /boot/efi
/dev/sdb1       3.9G   16M  3.7G   1% /mnt
/dev/sdc1        10G   43M   10G   1% /datadrive

Also, To ensure that the drive is remounted after a reboot, it must be added to the /etc/fstab file. To do so, I got the UUID of the disk with the 'blkid' utility input code

sudo -i blkid

UUID Output

UUID="b70183ff-8455-43a4-88c4-d19302d791ed" TYPE="xfs"

I then opened the /etc/fstab file in a text editor using the code input

sudo nano /etc/fstab

Of i added the line of code below 

UUID=b70183ff-8455-43a4-88c4-d19302d791ed   /datadrive  xfs    defaults,nofail   1  2

I then exited


7. TAKE A DISK SNAPSHOT

Before taking snapshot i created a disk ID using the code input

osdiskid=$(az vm show 
-g JesmykelRG1 -n myVM 
--query "storageProfile.osDisk.managedDisk.id" -o tsv)

I then use the code input to create a snapshot

az snapshot create 
--resource-group JesmykelRG1 
--source "$osdiskid" 
--name osDisk-backup

I then created a disk from snapshot using the code input

az disk create 
--resource-group JesmykelRG1 
--name Jesmykel 
--source osDisk-backup

I then restored vm from snapshot using the code input

az vm delete 
--resource-group JesmykelRG1 
--name myVM

I then created a new virtual machine from the snapshot disk using the code input

az vm create 
--resource-group JesmykelRG1 
--name myVM 
--attach-os-disk mySnapshotDisk 
--os-type linux

I then reattach the data disk using the code input after finding the data disk name using the code input below

datadisk=$(az disk list -g JesmykelRG1 --query "[?contains(name,'myVM')].[id]" -o tsv)

az vm disk attach 
–g JesmykelRG1 
--vm-name myVM 
--name $datadisk

Notes:
Quickstart: Manage Azure disks

https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-disks
Quickstart for Bash in Azure Cloud Shell

https://docs.microsoft.com/en-us/azure/cloud-shell/quickstart