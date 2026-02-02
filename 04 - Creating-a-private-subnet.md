# Creating a Private Subnet

**Author:** Thomas Miller  
**Email:** tmiller1996.work@gmail.com

---

## Creating a Private Subnet

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-private_afe1fdbd)

---

## Introducing Today's Project!

In today's project, I used Amazon VPC to create a private subnet. Additionally, created a route table and network ACL for the private subnet to make sure that it was not accessible externally.

### This project took me...

This project took me approximately 30 minutes.

---

## Private vs Public Subnets

The difference between public and private subnets is that public subnets can be accessed via the internet whereas private subnets can only be accessed within the VPC.

Having private subnets are useful because it can be utilized to store sensitive data such as a database of user passwords.

My private and public subnets cannot have the same CIDR so traffic is routed correctly and there are no conflicts.

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-private_afe1fdbd)

---

## A dedicated route table

By default, my private subnet is associated with the VPC's main route table. When you create a VPC, AWS automatically creates a main route table and any subnets within the VPC will use it.

I had to set up a new route table because the route table for the public subnet is connected to a IGW.

My private subnet's dedicated route table only has one inbound and one outbound rule that allows local traffic.

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-private_b4b904b5)

---

## A new network ACL

By default, my private subnet is associated with the VPCs Network ALC rules that are created when the VPC is created.

I set up a dedicated network ACL for my private subnet because the initial ACL inbound and outbound rules allow all traffic types.

My new network ACL has two simple rules - deny all inbound and outbound traffic. Creating a new ACL will automatically apply these rules. I also had to associate this ACL with the private subnet that I have created in order for the deny rules to apply.

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/aws-networks-private_1ed2cb07)

---

