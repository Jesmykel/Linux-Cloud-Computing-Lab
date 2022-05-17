# Lab 4: Create and use an SSH public-private key pair for Linux VMs in Azure

Task:

1. SUPPORTED SSH KEY FORMAT

I checked for supported ssh key formats on (https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys)

2. CREATE AN SSH KEY PAIR

To create an ssh key pair, i used the code input 

ssh-keygen -m PEM -t rsa -b 4096

After which i got the output below

Generating public/private rsa key pair.
Enter file in which to save the key (/home/segun/.ssh/id_rsa): mykeypair
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in mykeypair.
Your public key has been saved in mykeypair.pub.
The key fingerprint is:
SHA256:uOJxC5PpBOL0/lnqU0KP9D3HUaw2Eob8hZ+jSCvUt4Y segun@cc-1574-3254f253-765876bcb8-hzddl
The key's randomart image is:
+---[RSA 4096]----+
|      . . . .    |
|       o + . o   |
|      . o + +    |
|     + + + O     |
|... + * S * +    |
|o... * E * o     |
| . .O *.. o      |
|  .+ B+.         |
|   .==o          |
+----[SHA256]-----+

3. PROVIDE AN SSH PUBLIC KEY WHEN DEPLOYING A VM 

To provide ssh public key, i firstly displayed the ssh key using the code input 

cat Jesmykel.pub

The below output is displayed

ssh-rsa 
AAAAB3NzaC1yc2EAAAADAQABAAACAQDDV/BbJ0ID/ruuKsLaG7f3q4430iwZqvMFDsITM8pg/b/nfDjw1/rFKT+r2LLtz2rQTulAcZwYVpgjrsAgd+gSvgGiI5erGHXfgfp3XXyEowLLp7StaHUWcpOaJjXkK7yhUrh/+6jp/kJlBp6TpS8HluztLKCvi0ThGLXnNj8q0G4H2TANlmvMSbuHircriIt95R8nh3CGBVUWEDc0EfKBJcQ+Ks77hkcQA5N+lyHrOhAyQbq1dOVwqT4nhK2icdj1HrEuAlrZkLOUN2J1cfBCoROsKZvaMxfw+QTSHh6C6WV3OAvMJ+ZgkijQl8p19H3Fw8WE5o1XT1eD4CgHkgQcsFTFwSblWFbyf5OTmeLI96hXcjqnp7WcUQr4VJevOdPCDWtWki6ZEabatvX3Z/AuB4K8wV0rAVrKjl6XO6nxX6jGnM8CU6s/lwNsXQZJC5qXAus0joGqKqg7rllASSfXJiP2MCQSu9O/LAJud6s0QUsJa6KAhQ4Fv0spHfmR7y/zmrLdTY/VkyYr5mBayC9iDTXBaUqBwO/4mNrcjNTGQTH1A7dVKrIu7E86ehqsYmdqw6CcrLQoO24XDbw9h5PjWu1P+7miwf6umJZOmtOLNWy9dg4VEae2aAsAkOenXHT1A8W97s/5il5xnAvWymmdyNnb1ZZZzN14vjxDsVcjEQ== segun@cc-1574-3254f253-765876bcb8-hzddl

az vm create --resource-group JesmykelRG2 --name JesmykelVM --image UbuntuLTS --admin-username jesmykel --ssh-key-values mykeypair.pub


{
  "fqdns": "",
  "id": "/subscriptions/66edf686-e1a0-4369-ba02-98d34c1aec49/resourceGroups/JesmykelRG2/providers/Microsoft.Compute/virtualMachines/JesmykelVM",
  "location": "australiaeast",
  "macAddress": "00-22-48-94-5F-2D",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "20.213.125.109",
  "resourceGroup": "JesmykelRG2",
  "zones": ""
}

4. SSH INTO YOUR VM

To enter ssh into VM, I enter the input code

The below output was displayed

ssh -i mykeypair jesmykel@20.213.125.109

Enter passphrase for key 'mykeypair': 
Welcome to Ubuntu 18.04.6 LTS (GNU/Linux 5.4.0-1078-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Tue May 17 13:49:32 UTC 2022

  System load:  0.0               Processes:           108
  Usage of /:   4.8% of 28.90GB   Users logged in:     0
  Memory usage: 5%                IP address for eth0: 10.0.0.4
  Swap usage:   0%

0 updates can be applied immediately.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.


Notes:
Quickstart: SSH for Linux VMs

https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys
Quickstart for Bash in Azure Cloud Shell

https://docs.microsoft.com/en-us/azure/cloud-shell/quickstart