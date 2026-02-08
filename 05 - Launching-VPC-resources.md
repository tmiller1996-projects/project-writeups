# Launching VPC Resources

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-ec2)

**Author:** Thomas Miller  
**Email:** tmiller1996.work@gmail.com

---

## Launching VPC Resources

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-ec2_8ee57662)

---

## Introducing Today's Project!

### How I used Amazon VPC in this project

I used Amazon VPC to create EC2 instances in my public and private subnets. Additionally, I used the VPC Wizard in order to quickly create a VPC with a set of subnets, route tables, and internet gateways.

### This project took me...

This project took me approximately 45 minutes to complete.

---

## Setting Up Direct VM Access

Directly accessing a EC2 instance means logging into and managing the operating system or software of the machine as if you were using it in front of you, but over the internet.

### SSH is a key method for directly accessing a VM

SSH (Secure Shell) is a protocol used for secure remote access to the services we have just span up. It will utilize the public/private key pair that we generated previously. SSH is extremely common and is the standard way for developers to securely log in from their computer to another remote computer (e.g., an EC2 instance).

We're starting to see organization steer away from the implementation of SSH as IaC (Infrastructure as Code) becomes more popular. This is to reduce human interactions with systems and therefore reduce human error.

### To enable direct access, I set up key pairs

Key pairs are two cryptographic keys: one private and one public. The public key is installed on the virtual machine, and the private key remains with the user. When you attempt to connect, the machine uses the public key to create an encrypted challenge that can only be decrypted with the private key. Key pairs make sure that access to your EC2 instances is secure and authenticated.

I used RSA (Rivest-Shamir-Adleman), which is one of the most common cryptographic algorithms used due to its strength and security. RSA is widely supported and trusted for creating digital signatures and encrypting data.

My private key's file format is a .pem, which stands for Privacy Enhanced Mail. It actually started off as a way to secure emails but has since become the go-to format for managing cryptographic keys because it is supported by many different types of servers e.g. EC2 instances!

---

## Launching a public server

I had to change my EC2 instance's networking settings by specifying the VPC I want it to sit under, specifying the subnet within that VPC, and then specifying the security group within that subnet. I could also select at this point if I want it to auto-assign a public IP address.

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-ec2_88727bef)

---

## Launching a private server

My private server has its own dedicated security group because they have different exposure levels and different responsibilities. The public security group will allows traffic fron anywhere whereas the private security group will only allow traffic from the public subnet.

My private server's security group's source is the public subnet security group which means that my private subnet only trusts traffic coming from the public subnet security group. Specifially just SSH in this instance.

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-ec2_4a9e8014)

---

## Speeding up VPC creation

I used an alternative way to set up an Amazon VPC! This time, when going into the "Create VPC" menu, i chose the "VPC and more" option. This provided me with a way to auto-generate names, select CIDR blocks, customize AZs, choose the number of public/private subnets, implement NAT gateways, and setup VPC endpoints.

A VPC resource map is visualisation of what is included within a VPC. Logically, it will consist of the VPC itself, the Subnets, Route tables, and Network Connections. The resource map does not provide any details of security groups or ACLs.

My new VPC has a CIDR block of 10.0.0.0/16. It is possible for my new VPC to have the same IPv4 CIDR block as my existing VPC because AWS VPCs are isolated from each other by default, so there won't be any IP conflicts unless you explicitly connect them using VPC peering - will explore this at a later date.

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-ec2_1cbb1b88)

---

## Speeding up VPC creation

### Tips for using the VPC resource map

When determining the number of public subnets in my VPC, I only had two options: 0 or 2. This was because I had 2 AZs selected. If I had 3 AZs selected then I would be able to choose between 0 or 3. This is for redundancy purposes.

The set up page also offered to create NAT gateways, which are Network Address Translation gateways and are used by a private subnet in order to communicate outwards towards the internet while not assigning the service a public IP address. This hides the services from external exposure while still allowing it to communicate outwards for updates, for example.

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-ec2_8ee57662)

---

---

