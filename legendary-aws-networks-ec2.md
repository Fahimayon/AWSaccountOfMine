<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Launching VPC Resources

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-ec2)

**Author:** MD. Fahim Parvez  
**Email:** parvez22205341185@diu.edu.bd

---

## Launching VPC Resources

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-ec2_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a logically isolated virtual network in AWS where you can launch, organize, and manage cloud resources such as EC2 instances, databases, and load balancers.

It is useful because it allows you to control IP addressing, subnets, routing, and security, giving you a secure and customizable environment for both public and private resources.

### How I used Amazon VPC in this project

I used Amazon VPC to create a secure and isolated network environment where I could launch public and private subnets, configure route tables, attach an Internet Gateway, set up security groups and network ACLs, and deploy EC2 instances, ensuring proper traffic flow and access control.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how many different components—subnets, route tables, Internet Gateways, security groups, NACLs, and key pairs—need to work together to make a VPC fully functional and secure. And also how easy it was to create VPC resources using Amazon VPC's wizard, before it took some time to set it up.

### This project took me...

This project took me about 1.5 hours to complete

---

## Setting Up Direct VM Access

Directly accessing a virtual machine means connecting straight to the operating system of the instance (for example, via SSH for Linux or RDP for Windows) without going through an intermediary service or application, allowing you to manage, configure, and troubleshoot the system directly.

### SSH is a key method for directly accessing a VM

SSH traffic means network traffic used by the Secure Shell (SSH) protocol to securely connect to and manage a remote system over an encrypted connection, typically on port 22.

### To enable direct access, I set up key pairs

Key pairs are a set of cryptographic keys used to securely authenticate and access EC2 instances, typically consisting of a public key and a private key.

The public key is stored on the EC2 instance.

The private key is kept by the user and used to log in (for example, via SSH).

A private key’s file format means the specific file type used to store the cryptographic key, which determines how it can be used by authentication tools like SSH.

My private key’s file format was a .pem file, which is commonly used to securely connect to Linux EC2 instances using SSH.

---

## Launching a public server

I had to change my EC2 instance's networking settings by following:

1. Selecting NextWork VPC from the drop-down in the VPC list.

2. Select my public subnet.

3. For the Firewall (security groups), I've already created the security group for my public subnet's resources. Choose Select existing security group.

4. Select NextWork Public Security Group.

5. Lastly, launch an EC2 instance.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-ec2_88727bef)

---

## Launching a private server

My private server has its own dedicated security group because it allows me to tightly control access by permitting only specific traffic (such as SSH from the public EC2 instance) and blocking all other inbound connections, ensuring stronger security for sensitive backend resources.

My private server's security group's source is my Public Security Group, which means only EC2 instances that belong to the public security group are allowed to initiate traffic (such as SSH) to the private server, instead of allowing access from any IP address.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-ec2_4a9e8014)

---

## Speeding up VPC creation

I used an alternative way to set up an Amazon VPC! This time, I used the Amazon VPC wizard instead of manually creating each component, which allowed me to quickly launch a fully configured VPC with subnets, route tables, security groups, and an Internet Gateway in just a few clicks.

A VPC resource map is a visual or documented representation of all the resources in a VPC, such as subnets, route tables, Internet Gateways, security groups, network ACLs, and EC2 instances, showing how they are connected and how traffic flows between them.

My new VPC has a CIDR block of 10.0.0.0/16.

It is possible for my new VPC to have the same IPv4 CIDR block as my existing VPC because VPCs are logically isolated from each other, so IP addresses do not conflict across different VPCs, even if they use the same CIDR block.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-ec2_1cbb1b88)

---

## Speeding up VPC creation

### Tips for using the VPC resource map

When determining the number of public subnets in my VPC, I only had two options: one per Availability Zone.

This was because AWS requires that each subnet resides entirely within a single Availability Zone, so the number of public subnets depends on how many AZs you want to use for redundancy and high availability.

The setup page also offered to create NAT gateways, which are network devices that allow instances in private subnets to access the internet (for updates or external services) without exposing them directly to incoming internet traffic.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-ec2_8ee57662)

---

---
