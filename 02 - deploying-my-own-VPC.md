

# Building a Virtual Private Cloud


**Author:** Thomas Miller  
**Email:** tmiller1996.work@gmail.com


---

## Build a Virtual Private Cloud (VPC)

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-vpc_2facf927)

---

## Introducing Today's Project!

In this project, I will be developing my understanding of VPCs (Virtual Private Clouds) on AWS. I'm doing this project to learn more about VPC implementation, Public Subnets, and creatiner Internet Gateways

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is basically your own private network in the AWS cloud. It gives you full control over your cloud networking environment, similar to having your own on-premises data center but with the flexibility and scalability of the cloud. You are also able to choose whether you want it to be a public/private cloud in regard to connectivity.

In today's project, I used Amazon VPC to create a subnet with a set CIDR that was able to connect to the internet via an Internet Gateway

### Personal reflection

This project took me approximately 1 hour to complete

One thing I didn't expect in this project was the amount of flexibility available when it comes to implementing your own subnet.

---

## Virtual Private Clouds (VPCs)

### What I did in this step

In this step, I will be creating an IAM user for this project for security purposes. A root account should not be used for everday tasks as security breaches of credentials are more impactful than of a IAM user.

I will be accessing the IAM service, selecting the users section, and creating a used called "tmiller-IAM-admin"

### How VPCs work

A Virtual Private Cloud (VPC) is a private section of a public cloud that is logically isolated from other users. It gives you many of the benefits of having your own data center like security, control, and network customization without needing to own physical infrastructure.

### Why there is a default VPC in AWS accounts

AWS provides a default VPC to allow users to quickly setup services that they require. The majority of sevices used on AWS such EC2 require a VPC in order to be utilized. Some services such as Lambda and Amazon S3 do not require a VPC to use.

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-vpc_2facf927)

### Defining IPv4 CIDR blocks

To set up my VPC, I had to define an IPv4 CIDR block, which I have set to 10.0.0.0/16 meaning the range of IP address available is from 10.0.0.0 - 10.0.255.255. I've also specified no IPv6 CIDR block as IPv6 is not a requirement of this project.

---

## Subnets

### What I did in this step

Next I will be creating a subnet within my VPC

### Creating and configuring subnets

Subnets are a segmentation of the VPC's IP address range that then allows me to organize and isolate resources will my VPC.  There are already subnets existing in my account, one for every Availability Zone (AZ) within eu-north-1 (Stockholm)

### Public vs private subnets

The difference between public and private subnets are that private subnets do not have direct internet access. For a subnet to be considered public, it has to be connected to the internet/ This can be done via an Internet Gateway

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-vpc_157c4219)

### Auto-assigning public IPv4 addresses

Once I created my subnet, I enabled auto-assign public IPv4 address.  This setting makes sure any service that is span up within the subnet is automatically assigned a public address so th it is accessible from the internet and I don't have to create one manually.

---

## Internet gateways

### What I did in this step

So far, I've establish a VPC, created a subnet within that VPC, and enabled auto-assign public IPv4 addresses. The next step is to attach the VPC to an Internet Gateway in order to provide internet connectivity on ingress and egress.

### Setting up internet gateways

An Internet Gateway allows resources in your cloud network to communicate with the Internet. As the name suggests, its ultimately a doorway between the VPC and the public internet. Its implementation is extremely flexible allowing it to be horizontally scaled.

Attaching an internet gateway to a VPC means resources in my VPC can now access the internet. As previously mentioned, if this step was not included the services running inside the VPC would not be reachable from outside the VPC environment.

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-vpc_4ae90410)

---

## Using the AWS CLI

### What I'm doing in this extension

To extend this project, im going to use the AWS CLI to launch the VPC resources.

### Exploring CloudShell and CLI

VPC resources could also be created with CloudShell, which is the Command Line Interface (CLI) that AWS supports.

Here is the command used to setup a VPC:
```
aws ec2 create-vpc --cidr-block 10.0.0.0/24 --query Vpc.VpcId --output text
```
Interestingly, VPCs were originally designed for setting up private networks for EC2 instances! VPCs are now essential for a wider range of services, but they were initially tied to EC2, so their CLI commands still start with 'aws ec2'.

### Adding a Subnet

To set up a subnet for my VPC, I used the command:
```
aws ec2 create-subnet --vpc-id "VPC-ID" --cidr-block 10.0.0.0/25
```
### Adding an Internet Gateway

To create the IG I used the command:
```
aws ec2 create-internet-gateway --query InternetGateway.InternetGatewayId --output text
```
To add IG to the VPC I used:
```
aws ec2 attach-internet-gateway --vpc-id VPC-ID --internet-gateway-id IG-ID
```
### Comparing CloudShell vs AWS Console

Compared to using the AWS Console, an advantage of using CloudShell is that it is a lot faster to create a VPC An advantage of using the Console is that you are able to see all of the customization options and visualisations of resource mapping.

Overall, from a learning perspective, I preferred the manual process of going through menus so I knew what options were available. As I become more familiar with Cloud environments the CLI will be a lot faster.

---

---
