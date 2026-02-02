# VPC Traffic Flow and Security

**Author:** Thomas Miller  
**Email:** tmiller1996.work@gmail.com

---

## VPC Traffic Flow and Security

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-security_92b0b0b4)

---

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC in conjunction with an already setup Subnet and IGW to create route tables, network ACLs, and Security groups.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how easy it was to setup rules through the AWS Console.

### This project took me...

This project took me approximately 50 minutes.

---

## Route tables

Route tables are essentially a list of traffic rules for the VPC. They direct traffic based on the IP addresses used. Each route typically containts a Destination (CIDR format) and a Target (e.g. IGW, VPN, etc..).

Routes tables are needed to make a subnet public because a subnet is only public if its route table sends internet traffic to an Internet Gateway. A subunet is considered public if its associated route table contains a default route to an internet gateway because routing determines whether traffic can leave the VPC and reach the internet.wwww

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-security_0a07b191)

---

## Route destination and target

Routes are defined by their destination and target, which means the destination is where traffic is trying to go and the target is where the traffic will be sent next.

```
10.0.0.0/16 - Inside this VPC
0.0.0.0/0 - The internet
```

The route in my route table that directed internet-bound traffic to my internet gateway had a destination of 0.0.0.0/0 and a target of the internet gateway as previously specified.

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-security_0a07b191)

---

## Security groups

![Image](https://learn.nextwork.org/projects/static/aws-networks-security/high-step3.0.png)

### Inbound vs Outbound rules

Inbound rules are for traffic coming into the VPC. I  configured an inbound rule that allows all HTTP traffic from the internet to be able to access the VPC. AWS does warn you for setting up this rule with an CIDR of 0.0.0.0/0 but this is required if you want anyone with an internet connection to access your VPC 

Outbound rules are rules that allow traffic to leave the VPC. By default, AWS security group's outbound rule are set to always allow outbound traffic.

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-security_92b0b0b4)

---

## Network ACLs

Network ACLs are a broad set of rules that are applied to a specific subnet.

### Security groups vs. network ACLs

The difference between a security group and a network ACL is that security groups apply to a specific EC2 instances within the subnet. network ACL is a generalized list of rules for the entire subnet.

---

## Default vs Custom Network ACLs

### Similar to security groups, network ACLs use inbound and outbound rules

By default, a network ACL's inbound and outbound rules will allow all traffic. This is often set at rule 100 within the rules table.

In contrast, a custom ACL’s inbound and outbound rules are automatically set to deny all by default.

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-security_4faeb056)

---

## Tracking VPC Resources

---

---
