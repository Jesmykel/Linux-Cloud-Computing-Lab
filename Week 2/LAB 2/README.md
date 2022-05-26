# Lab 2: Manage Linux VMs with the AWS CLI


1. Create virtual machine
To create a VM (instance) i used an alraedy existing keypair, and VPC, I then used the code input

aws ec2 run-instances 
--image-id ami-07d02ee1eeb0c996c 
--count 1 
--instance-type t2.micro 
--key-name seg 
--security-group-ids sg-0fcd61ad8f59f4e2c


2. Connect to VM

To connect to my VM, i opened port 22 and port 80 using the code input, the went back to the management management console to use the Ec2 connect to connect my instance
NB: The security i used already have port 22 and 80 opened already, so i just connected directly from the management console.

3. Understand VM images

To understander VM images, i visited (https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.customenv.html)

4. Understand VM sizes

To understand VM sizes, i visited (https://docs.aws.amazon.com/cli/latest/reference/rds/create-db-instance.html?highlight=instance%20sizes)

5. VM power states
To view VM power state i used the input code

aws ec2 describe-instance-status --instance-id i-06d5f695a181a2f2f

And i got the output

{
    "InstanceStatuses": [
        {
            "AvailabilityZone": "us-east-1b",
            "InstanceId": "i-06d5f695a181a2f2f",
            "InstanceState": {
                "Code": 16,
                "Name": "running"
            },
            "InstanceStatus": {
                "Details": [
                    {
                        "Name": "reachability",
                        "Status": "passed"
                    }
                ],
                "Status": "ok"
            },
            "SystemStatus": {
                "Details": [
                    {
                        "Name": "reachability",
                        "Status": "passed"
                    }
                ],
                "Status": "ok"
            }
        }
    ]
}


6. Management tasks

I performed the following management tasks
> Reboot instance
> Terminate instance
> Stop Instance

To reboot instance i used the input code
aws ec2 reboot-instances --instance-ids i-06d5f695a181a2f2f

To terminate instance i used the input code
aws ec2 terminate-instances --instance-ids i-06d5f695a181a2f2f

And the below output was displayed
{
    "TerminatingInstances": [
        {
            "CurrentState": {
                "Code": 32,
                "Name": "shutting-down"
            },
            "InstanceId": "i-06d5f695a181a2f2f",
            "PreviousState": {
                "Code": 16,
                "Name": "running"
            }
        }
    ]
}

To stop instance i used the input code

aws ec2 stop-instances --instance-ids i-06d5f695a181a2f2f

And the output below was displayed

{
    "StoppingInstances": [
        {
            "InstanceId": "i-06d5f695a181a2f2f",
            "CurrentState": {
                "Code": 64,
                "Name": "stopping"
            },
            "PreviousState": {
                "Code": 16,
                "Name": "running"
            }
        }
    ]
}






Notes:
Quickstart: Create a Linux VM

https://aws.amazon.com/getting-started/launch-a-virtual-machine-B-0/
Using a custom Amazon machine image (AMI)

https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.customenv.html
Quickstart: Restart VM via CLI

https://docs.aws.amazon.com/cli/latest/reference/ec2/reboot-instances.html
Quickstart for AWS CloudShell

https://docs.aws.amazon.com/cloudshell/latest/userguide/working-with-cloudshell.html