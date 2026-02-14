<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Peering

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-peering)

**Author:** MD. Fahim Parvez  
**Email:** parvez22205341185@diu.edu.bd

---

## VPC Peering

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-peering_88727bef)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a logically isolated virtual network in AWS where you can launch and manage cloud resources such as EC2 instances, databases, and load balancers.

It is useful because it allows you to control IP addressing, subnets, routing, and security, providing a secure and customizable environment for both public and private resources.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create and manage isolated network environments for multiple VPCs, configure subnets, route tables, security groups, and network ACLs, establish a VPC peering connection, and deploy EC2 instances to test private communication between VPCs.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was the level of detail required to make VPC peering work correctly.

### This project took me...

This project took me about two hours as I was documenting at the same time

---

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, I will use the Amazon VPC wizard and the visual VPC resource map to quickly create two separate VPCs from scratch because these tools automate the setup process and ensure that all required networking components are configured correctly in a fast and efficient way.

### Step 2 - Create a Peering Connection

In this step, I will create a VPC peering connection between my two VPCs because peering enables private, secure communication between isolated VPC networks without sending traffic over the public internet.

### Step 3 - Update Route Tables

In this step, I will update the route tables in both VPCs to add routes that point to the VPC peering connection because VPC peering does not automatically route traffic, and explicit routes are required for resources in each VPC to communicate with each other.

### Step 4 - Launch EC2 Instances

In this step, I will launch an EC2 instance in each VPC because these instances will act as test resources that allow me to verify and validate connectivity across the VPC peering connection.

---

## Multi-VPC Architecture

I started my project by launching two VPC's, and I have created one subnet in each VPC

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16. They have to be unique because VPC peering does not support overlapping IP address ranges, and unique CIDR blocks are required to correctly route traffic between the two VPCs without IP conflicts.

### I also launched 2 EC2 instances

I didn’t set up key pairs for these EC2 instances because I wasn’t planning to directly SSH into them, and they were only being used as test resources to verify network connectivity for the VPC peering setup.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-peering_11111111)

---

## VPC Peering

A VPC peering connection is a networking connection between two Amazon VPCs that allows resources in each VPC to communicate with each other privately using their private IP addresses, as if they were part of the same network.

VPCs would use peering connections to securely share resources and allow private communication between services running in different VPCs, without routing traffic over the public internet.

The difference between a Requester and an Accepter in a peering connection is that the Requester is the VPC that initiates the peering connection request, while the Accepter is the VPC that receives and approves the request before the connection becomes active.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-peering_1cbb1b88)

---

## Updating route tables

After accepting a peering connection, my VPCs' route tables need to be updated because VPC peering only creates the connection link and does not automatically modify routing, so each VPC must have explicit routes that direct traffic for the peer VPC’s CIDR block through the peering connection.

My VPCs' new routes have a destination of the CIDR block of the peer VPC 10.2.0.0/16 in VPC 1’s route table and 10.1.0.0/16 in VPC 2’s route table.

The routes' target was the VPC peering connection, which tells AWS to send traffic destined for the peer VPC through the peering link.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-peering_4a9e8014)

---

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step, I will use EC2 Instance Connect to connect to the EC2 instance in VPC 1 because I need command-line access to the instance in order to send network traffic and test connectivity to the EC2 instance in the peered VPC.

### Step 6 - Connect to EC2 Instance 1

In this step, I will use EC2 Instance Connect to try connecting to Instance 1 again because the previous connectivity issue was resolved by assigning an Elastic IP, and I need to successfully access the instance to continue testing the VPC peering setup.

### Step 7 - Test VPC Peering

In this step, I will send network traffic from Instance 1 in VPC 1 to Instance 2 in VPC 2 and troubleshoot any connection issues because successful communication between the two instances confirms that the VPC peering connection and routing have been configured correctly.

---

## Troubleshooting Instance Connect

Next, I used EC2 Instance Connect to securely access my first EC2 instance directly from the AWS Management Console without needing to manage SSH keys or configure a local SSH client.

I was stopped from using EC2 Instance Connect as the instance doesn't have a public IPv4 address

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-peering_7685490c)

---

## Elastic IP addresses

To resolvastice this error, I set up Elastic IP addresses. Elastic IP addresses are static, public IPv4 addresses provided by AWS that you can allocate to your account and associate with resources like EC2 instances, allowing them to be reached from the internet using a fixed IP address even if the instance is stopped and restarted.

Associating an Elastic IP address resolved the error because it has given the instance a public IPv4 address 

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-peering_45663498)

---

## Troubleshooting ping issues

To test VPC peering, I ran the command ping 10.2.6.118

A successful ping test would validate my VPC peering connection because it proves that network traffic can travel from one VPC to the other using private IP addresses, confirming that the peering connection, route tables, and security group rules are all correctly configured.

I had to update my second EC2 instance's security group because it was not allowing inbound traffic from the first EC2 instance, which prevented successful communication through the VPC peering connection.

I added a new rule that allowed inbound ICMP (for ping) or the required protocol from the security group of Instance 1, enabling traffic to flow between the two VPCs.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-peering_7a29d352)

---

---
