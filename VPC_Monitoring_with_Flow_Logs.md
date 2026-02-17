<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Monitoring with Flow Logs

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-monitoring)

**Author:** MD. Fahim Parvez  
**Email:** parvez22205341185@diu.edu.bd

---

## VPC Monitoring with Flow Logs

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-monitoring_3e1e79a1)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a logically isolated virtual network in AWS where you can launch and manage resources such as EC2 instances, databases, and load balancers.

It is useful because it allows you to control IP addressing, subnets, routing, and security, enabling secure and flexible management of cloud resources while isolating them from other networks.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to set up two isolated virtual networks, launch EC2 instances, establish a VPC peering connection, and configure VPC Flow Logs to monitor and analyze network traffic using CloudWatch.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how much insight VPC Flow Logs and CloudWatch Log Insights could provide about the network, including seeing which traffic was accepted, rejected, and which IPs were transferring the most data, even without directly accessing the instances.

### This project took me...

This project took me 2 hours 

---

## In the first part of my project...

### Step 1 - Set up VPCs

In this step, I will use the VPC wizard to quickly create two separate VPCs from scratch because it allows me to efficiently build a complete network foundation while revising key concepts like VPC isolation and peering, which are essential for monitoring traffic across multiple VPCs.

### Step 2 - Launch EC2 instances

In this step, I will launch one EC2 instance in each VPC because these instances will generate network traffic between the VPCs, allowing me to test the VPC peering connection and create real traffic data to monitor using VPC Flow Logs and CloudWatch.

### Step 3 - Set up Logs

In this step, I will enable VPC Flow Logs and configure them to send inbound and outbound traffic records to Amazon CloudWatch Logs because Flow Logs allow me to capture detailed network traffic information that I can later analyze to understand connectivity, performance, and security behavior within my VPCs.

### Step 4 - Set IAM permissions for Logs

In this step, I will create an IAM policy and role and attach them to my VPC Flow Log because VPC Flow Logs need explicit permissions to write network traffic records and send them to Amazon CloudWatch Logs.

---

## Multi-VPC Architecture

I started my project by launching two VPC's and I have created one subnets each for VPC's 

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16. They have to be unique because the VPC's IP cannot overlap 

### I also launched EC2 instances in each subnet

My EC2 instances' security groups allow all ICMP from IPv4 addresses or 0.0.0.0/0. This is because I need to check the connection between VPC instances using the ping command 

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-monitoring_e7fa8775)

---

## Logs

Logs are records of events or activities that happen in a system over time.

In cloud and networking contexts, logs capture what happened, when it happened, and where it happened, so engineers can review, analyze, and troubleshoot systems.

Log groups are containers in Amazon CloudWatch Logs that organize and store related log data in one place.

### I also set up a flow log for VPC 1

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-monitoring_e8398869)

---

## IAM Policy and Roles

I created an IAM policy because VPC Flow Logs need clearly defined permissions that specify what actions they are allowed to perform, such as creating log streams and writing network traffic data to Amazon CloudWatch Logs.

I also created an IAM role because VPC Flow Logs need a secure identity they can assume to use the permissions defined in the IAM policy and deliver log data to Amazon CloudWatch Logs.

A custom trust policy is a rule set that specifies which AWS service is trusted to assume an IAM role.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-monitoring_4334d777)

---

## In the second part of my project...

### Step 5 - Ping testing and troubleshooting

In this step, I will generate network traffic from Instance 1 in VPC 1 to Instance 2 in VPC 2 because sending traffic allows me to test both the VPC peering connection and the VPC Flow Logs setup, confirming that traffic is flowing correctly and being recorded for monitoring and analysis.

### Step 6 - Set up a peering connection

In this step, I will create a VPC peering connection between VPC 1 and VPC 2 and update their route tables because the previous ping test failed due to missing routing, and establishing the peering connection ensures that traffic can flow privately between the two VPCs.

### Step 7 - Analyze flow logs

In this step, I will analyze Flow Logs because they show how network traffic flows and whether security rules are working.

---

## Connectivity troubleshooting

My first ping test between my EC2 instances had no replies, which means that the network traffic was being blocked somewhere, most likely by the security group or network ACL rules on one or both of the instances, or that routing between the VPCs was not fully configured.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-monitoring_99d4ba42)

I could receive ping replies if I ran the ping test using the other instance's public IP address, which means that the instances could reach each other over the internet, but the VPC peering private connectivity was not yet fully allowed due to missing security group rules or route table entries.

---

## Connectivity troubleshooting

Looking at VPC 1's route table, I identified that the ping test with Instance 2's private address failed because the route table lacked a route to the peer VPC’s CIDR via the peering connection.

### To solve this, I set up a peering connection between my VPCs

I also updated both VPCs' route tables so that traffic destined for the other VPC’s CIDR block would be routed through the VPC peering connection, allowing EC2 instances in VPC 1 and VPC 2 to communicate privately using their private IP addresses.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-monitoring_7316a13d)

---

## Connectivity troubleshooting

I received ping replies from Instance 2's private IP address! This means that the VPC peering connection and route tables are correctly configured, and network traffic can now flow privately between the two VPCs as intended.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-monitoring_4ec7821f)

---

## Analyzing flow logs

Flow logs tell us about the network traffic in our VPC, including which resources are communicating, the source and destination IP addresses, ports, protocols, whether the traffic was accepted or rejected, and the amount of data transferred.

For example, the flow log I've captured tells us
Timestamp
2026-02-17T13:39:49.000Z
→ When the log entry was recorded (UTC).

Version
2
→ Flow log format version.

Account ID
232048051936
→ AWS account where this traffic occurred.

Network Interface
eni-0e29fa92efdd0bbd
→ The ENI attached to your instance/resource.

Source IP
45.79.177.245
→ External/public IP initiating the connection.

Destination IP
10.1.3.77
→ Private IP inside your VPC.

Source Port
35467
→ Ephemeral port from the external host.

Destination Port
261
→ Port on your instance (service being targeted).

Protocol
6
→ TCP (6 = TCP, 17 = UDP).

Packets
44
→ Number of packets attempted.

Bytes
1771335589? (values slightly blurred)
→ Amount of data involved.

Start / End Time
Epoch timestamps
→ When the traffic flow started and ended.

Action
REJECT
→ Important part: Traffic was blocked.

Log Status
OK
→ Logging worked correctly.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-monitoring_d116818e)

---

## Logs Insights

Log Insights is a feature of Amazon CloudWatch that allows you to query, analyze, and visualize log data stored in CloudWatch Logs, making it easier to understand patterns, troubleshoot issues, and gain insights from large volumes of log data.

I ran the query “Return Top 10 byte transfers by source and destination IP addresses.” This query analyzes the amount of data sent between different IP addresses in my VPC and identifies which sources and destinations are transferring the most traffic.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-monitoring_3e1e79a1)

---

---
