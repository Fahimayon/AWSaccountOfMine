<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Creating a Private Subnet

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-private)

**Author:** MD. Fahim Parvez  
**Email:** parvez22205341185@diu.edu.bd

---

## Creating a Private Subnet

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-private_afe1fdbd)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a logically isolated virtual network in AWS where you can launch and manage resources like EC2 instances, databases, and load balancers.

It is useful because it allows you to control IP addressing, routing, subnets, and security, giving you a secure and customizable environment for your cloud resources.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create an isolated network environment where I could launch private and public subnets, configure route tables, attach an Internet Gateway, and secure resources with security groups and network ACLs, ensuring controlled traffic flow and protection for sensitive resources.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project is how many layers of security and routing are involved in a VPC, and how even small misconfigurations in route tables, security groups, or NACLs can prevent resources from communicating properly.

### This project took me...

This project took me about an hour to complete, but also about 45 mins to document it and redo previous resources as I deleted those earlier 

---

## Private vs Public Subnets

The difference between public and private subnets is that a public subnet has a route to an Internet Gateway, allowing resources to communicate directly with the internet, while a private subnet does not have this route, keeping its resources isolated from direct internet access.

Having private subnets is useful because they keep sensitive resources isolated from the public internet, reducing the attack surface and improving security while still allowing controlled internal communication within the VPC.

My private and public subnets cannot have the same CIDR block (IP address range) because subnets within a VPC must have non-overlapping IP ranges to route traffic correctly.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-private_afe1fdbd)

---

## A dedicated route table

By default, my private subnet is associated with the main route table of the VPC until I explicitly associate it with a custom private route table.

I had to set up a new route table because the default (main) route table may include routes intended for public subnets, and creating a separate route table allows me to control traffic specifically for the private subnet and ensure it has no direct route to the Internet Gateway.

My private subnet's dedicated route table only has one inbound and one outbound rule that allows traffic within the VPC CIDR block (local), meaning resources in the private subnet can communicate internally but cannot send or receive traffic from the internet.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-private_b4b904b5)

---

## A new network ACL

By default, my private subnet is associated with the main route table of the VPC, which applies the default routing rules until I explicitly associate it with a custom private route table.

I set up a dedicated network ACL for my private subnet because it provides an extra layer of security at the subnet level, allowing me to control inbound and outbound traffic, block unwanted access from the internet, and protect sensitive resources such as databases and internal services.

My new network ACL has two simple rules, which are inbound and outbound roules both deny all traffic for now 

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-private_1ed2cb07)

---

---
