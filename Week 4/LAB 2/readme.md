## Launch an Amazon linux instance using AWS CLI

Tasks:

Launch an instance with the following property 
1. instance OS   - Amzon linux
2. instance type - t2.micro
3. Region: Oregon
4. Network: Lab VPC, Public Subnet
5. Tag:  Key: Name     Value: ProdCafeServer
6. Security Group:  Create a  one named serverSG, with TCP port 22 and port 80 open to anywhere

To launch an instance, I firstly created a key pair with the name "ProdCafeServer" and security group with the name "serverSG" with the code input

aws ec2 create-key-pair --key-name ProdCafeServer --query 'KeyMaterial' --output text > ProdCafeServer.pem

And

aws ec2 create-security-group --group-name serverSG --description "My security group" --vpc-id vpc-0b14b79b595a6ddff

So i then launch an instance with the properties stated above using the code input

 aws ec2 run-instances --image-id ami-0ca285d4c2cda3300 --count 1 --instance-type t2.micro --key-name ProdCafeServer --security-group-ids sg-012a14eedee37ae35 --subnet-id subnet-005c23d8427e2efbb

I then open port 22 and 80 with the code input

aws ec2 authorize-security-group-ingress --group-id sg-012a14eedee37ae35 --protocol tcp --port 22 --cidr 0.0.0.0/0

And

aws ec2 authorize-security-group-ingress --group-id sg-012a14eedee37ae35 --protocol tcp --port 80 --cidr 0.0.0.0/0

To associate elastic ip, i used the code input

aws ec2 allocate-address
aws ec2 associate-address --instance-id i-0e4c7391852ecd0fa --allocation-id eipalloc-03d116ca852e0d694





Hint: Associate an elastic ip with this instance, you will need it in later lab.


Grading tip:  Screenshot major cli output and upload with your step by step answer (AWS describe command can help)


Guide:

https://docs.aws.amazon.com/cli/latest/userguide/cli-services-ec2-instances.html
