# Lab 2: Manage Linux VMs with the Azure CLI

Task: 

1. Create resource group

I created a resource group with the input

az group create --name JesmykelRG1 --location Australiaeast
 
2. Create virtual machine

I created a virtual machine with the input 

az vm create --resource-group JesmykelRG1 --admin-username azureuser --image UbuntuLTS --name myVM --generate-ssh-keys

3. Connect to VM

I connected to a virtual machine using the code input

ssh azureuser@20.248.189.187

4. Understand VM images

 To view VM images i used the code input

az vm image list --output table

A list of various images were displayed 

Offer                         Publisher               Sku                 Urn                                                             UrnAlias             Version
----------------------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
CentOS                        OpenLogic               7.5                 OpenLogic:CentOS:7.5:latest                                     CentOS               latest
debian-10                     Debian                  10                  Debian:debian-10:10:latest                                      Debian               latest
flatcar-container-linux-free  kinvolk                 stable              kinvolk:flatcar-container-linux-free:stable:latest              Flatcar              latest
opensuse-leap-15-3            SUSE                    gen2                SUSE:opensuse-leap-15-3:gen2:latest                             openSUSE-Leap        latest
RHEL                          RedHat                  7-LVM               RedHat:RHEL:7-LVM:latest                                        RHEL                 latest
sles-15-sp3                   SUSE                    gen2                SUSE:sles-15-sp3:gen2:latest                                    SLES                 latest
UbuntuServer                  Canonical               18.04-LTS           Canonical:UbuntuServer:18.04-LTS:latest                         UbuntuLTS            latest
WindowsServer                 MicrosoftWindowsServer  2022-Datacenter     MicrosoftWindowsServer:WindowsServer:2022-Datacenter:latest     Win2022Datacenter    latest
WindowsServer                 MicrosoftWindowsServer  2019-Datacenter     MicrosoftWindowsServer:WindowsServer:2019-Datacenter:latest     Win2019Datacenter    latest
WindowsServer                 MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer                 MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer                 MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
WindowsServer                 MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest

5. Understand VM sizes

To view VM sizes i used the code input

az vm list-sizes --location Australiaeast --output table

Several VM sizes were displayed, below is a list of few

MaxDataDiskCount    MemoryInMb    Name                    NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
4                   8192          Standard_D2ds_v4        2                1047552           76800
8                   16384         Standard_D4ds_v4        4                1047552           153600
16                  32768         Standard_D8ds_v4        8                1047552           307200
32                  65536         Standard_D16ds_v4       16               1047552           614400
32                  131072        Standard_D32ds_v4       32               1047552           1228800
32                  196608        Standard_D48ds_v4       48               1047552           1843200
32                  262144        Standard_D64ds_v4       64               1047552           2457600
4                   8192          Standard_D2ds_v5        2                1047552           76800
8                   16384         Standard_D4ds_v5        4                1047552           153600
16                  32768         Standard_D8ds_v5        8                1047552           307200
32                  65536         Standard_D16ds_v5       16               1047552           614400
32                  131072        Standard_D32ds_v5       32               1047552           1228800
32                  196608        Standard_D48ds_v5       48               1047552           1843200
32                  262144        Standard_D64ds_v5       64               1047552           2457600
32                  393216        Standard_D96ds_v5       96               1047552           3686400
4                   8192          Standard_D2d_v4         2                1047552           76800
8                   16384         Standard_D4d_v4         4                1047552           153600
16                  32768         Standard_D8d_v4         8                1047552           307200
32                  65536         Standard_D16d_v4        16               1047552           614400
32                  131072        Standard_D32d_v4        32               1047552           1228800
32                  196608        Standard_D48d_v4        48               1047552           1843200


6. VM power states

To check VM power state I inputed the code input

az vm get-instance-view --name myVM --resource-group JesmykelRG1 --query instanceView.statuses[1] --output table

The below code output was displayed

Code                Level    DisplayStatus
------------------  -------  ---------------
PowerState/running  Info     VM running


7. Management tasks

Several management tasks can be carried out in a vm which include
> Obtaining IP address
> Stoping a VM
> Strating a VM
> Deleting a VM

I carried out the above management task on my VM

> Obtaining IP address
I used the input code

az vm list-ip-addresses --resource-group JesmykelRG1 --name myVM --output table

The below code output was displayed

VirtualMachine    PublicIPAddresses    PrivateIPAddresses
----------------  -------------------  --------------------
myVM              20.248.189.187       10.0.0.4


> Stopping a VM
I stopped my VM using the input code

az vm stop --resource-group JesmykelRG1 --name myVM

> Starting a VM
I then restarted it using the code input

az vm start --resource-group JesmykelRG1 --name myVM

> Deleting a VM
I them deleted my VM using the input code

az group delete --name JesmykelRG1 --no-wait --yes

Notes:
Quickstart: Create a Linux VM

https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-vm
Quickstart for Bash in Azure Cloud Shell

https://docs.microsoft.com/en-us/azure/cloud-shell/quickstart