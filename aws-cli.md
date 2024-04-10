# AWS CLI Commands

Comprehensive Linux script that incorporates the creation of a VPC, subnets, an internet gateway, a security group, a network ACL (NACL), and an EC2 instance with the latest Amazon Linux AMI. The script also installs an Apache web server on the EC2 instance.

```bash
#!/bin/bash

# Define variables
REGION="us-west-2" # Change to your desired AWS region
VPC_CIDR="10.0.0.0/16"
PUBLIC_SUBNET_CIDR="10.0.1.0/24"
PRIVATE_SUBNET_CIDR="10.0.2.0/24"
AMI_NAME="/aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2"

# Fetch the latest Amazon Linux AMI ID
AMI_ID=$(aws ssm get-parameters --names $AMI_NAME --region $REGION --query 'Parameters[0].Value' --output text)

# Create VPC
VPC_ID=$(aws ec2 create-vpc --cidr-block $VPC_CIDR --query 'Vpc.VpcId' --output text)

# Create Public Subnet
PUBLIC_SUBNET_ID=$(aws ec2 create-subnet --vpc-id $VPC_ID --cidr-block $PUBLIC_SUBNET_CIDR --availability-zone ${REGION}a --query 'Subnet.SubnetId' --output text)

# Create Private Subnet
PRIVATE_SUBNET_ID=$(aws ec2 create-subnet --vpc-id $VPC_ID --cidr-block $PRIVATE_SUBNET_CIDR --availability-zone ${REGION}a --query 'Subnet.SubnetId' --output text)

# Create Internet Gateway
INTERNET_GATEWAY_ID=$(aws ec2 create-internet-gateway --query 'InternetGateway.InternetGatewayId' --output text)
aws ec2 attach-internet-gateway --internet-gateway-id $INTERNET_GATEWAY_ID --vpc-id $VPC_ID

# Create a Route Table for the Public Subnet
ROUTE_TABLE_ID=$(aws ec2 create-route-table --vpc-id $VPC_ID --query 'RouteTable.RouteTableId' --output text)
aws ec2 create-route --route-table-id $ROUTE_TABLE_ID --destination-cidr-block 0.0.0.0/0 --gateway-id $INTERNET_GATEWAY_ID
aws ec2 associate-route-table --route-table-id $ROUTE_TABLE_ID --subnet-id $PUBLIC_SUBNET_ID

# Create a Security Group
SECURITY_GROUP_ID=$(aws ec2 create-security-group --group-name MySecurityGroup --description "Security group for SSH and HTTP access" --vpc-id $VPC_ID --query 'GroupId' --output text)
aws ec2 authorize-security-group-ingress --group-id $SECURITY_GROUP_ID --protocol tcp --port 22 --cidr 0.0.0.0/0
aws ec2 authorize-security-group-ingress --group-id $SECURITY_GROUP_ID --protocol tcp --port 80 --cidr 0.0.0.0/0

# Create a Network ACL
NETWORK_ACL_ID=$(aws ec2 create-network-acl --vpc-id $VPC_ID --query 'NetworkAcl.NetworkAclId' --output text)
aws ec2 create-network-acl-entry --network-acl-id $NETWORK_ACL_ID --ingress --rule-number 100 --protocol tcp --port-range From=22,To=22 --cidr-block 0.0.0.0/0 --rule-action allow
aws ec2 create-network-acl-entry --network-acl-id $NETWORK_ACL_ID --ingress --rule-number 110 --protocol tcp --port-range From=80,To=80 --cidr-block 0.0.0.0/0 --rule-action allow
aws ec2 create-network-acl-entry --network-acl-id $NETWORK_ACL_ID --egress --rule-number 100 --protocol tcp --port-range From=0,To=65535 --cidr-block 0.0.0.0/0 --rule-action allow

# Launch an EC2 Instance in the Public Subnet
INSTANCE_ID=$(aws ec2 run-instances --image-id $AMI_ID --count 1 --instance-type t2.micro --key-name MyKeyPair --security-group-ids $SECURITY_GROUP_ID --subnet-id $PUBLIC_SUBNET_ID --query 'Instances[0].InstanceId' --output text)

# Install Apache Web Server on the EC2 Instance
aws ec2 wait instance-running --instance-ids $INSTANCE_ID
PUBLIC_IP=$(aws ec2 describe-instances --instance-ids $INSTANCE_ID --query 'Reservations[0].Instances[0].PublicIpAddress' --output text)
ssh -i /path/to/your/key.pem ec2-user@$PUBLIC_IP "sudo yum install -y httpd && sudo systemctl start httpd && sudo systemctl enable httpd"
```

**Detailed Explanation:**

| **Step** | **Description** |
| --- | --- |
| **Variables** | Set your AWS region and define the CIDR blocks for your VPC and subnets. |
| **Fetch AMI ID** | Use the AWS Systems Manager Parameter Store to get the latest Amazon Linux AMI ID. |
| **Create VPC** | Establish a new VPC with the specified CIDR block. |
| **Create Subnets** | Create both public and private subnets within the VPC. |
| **Internet Gateway** | Set up an internet gateway and attach it to the VPC for internet access. |
| **Route Table** | Create a route table for the public subnet and add a default route to the internet gateway. |
| **Security Group** | Create a security group with rules to allow SSH and HTTP traffic. |
| **Network ACL** | Set up a network ACL with rules to allow inbound SSH and HTTP traffic, and allow all outbound traffic. |
| **Launch EC2 Instance** | Start an EC2 instance in the public subnet with the latest AMI. |
| **Install Apache** | Once the instance is running, connect via SSH and install the Apache web server. |

Make sure to replace placeholder values like `MyKeyPair` and `/path/to/your/key.pem` with your actual key pair name and private key file path. Also, ensure that your AWS CLI is configured with the necessary permissions to execute these commands. If you encounter any issues, check your IAM user permissions and AWS CLI configuration.
