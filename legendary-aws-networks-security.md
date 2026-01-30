<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Traffic Flow and Security

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-security)

**Author:** MD. Fahim Parvez  
**Email:** parvez22205341185@diu.edu.bd

---

## VPC Traffic Flow and Security

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-security_92b0b0b4)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a logically isolated virtual network in AWS where you can launch and manage cloud resources like EC2 instances, databases, and load balancers.

It is useful because it allows you to control IP addressing, subnets, routing, and security, providing a secure and customizable environment for your resources.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create an isolated network environment where I could launch subnets, configure routing, set up an Internet Gateway, and secure resources with security groups and NACLs, ensuring proper traffic flow and controlled access within my AWS environment.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how many components and layers of security and routing are involved in a VPC, and how each setting—like route tables, security groups, and NACLs—directly affects traffic flow and resource accessibility.

### This project took me...

This project took me about an hour to complete, but I was documenting the same time, so it took about 1.5 hours 

---

## Route tables

Route tables are VPC components that control how network traffic is directed within and outside a VPC.
What route tables do

A route table contains rules (routes) that determine:

Where traffic is sent based on destination IP ranges

Whether traffic stays inside the VPC or goes outside (e.g., to the internet)

Each route has:

Destination (CIDR block, e.g. 0.0.0.0/0)

Target (IGW, NAT Gateway, VPC peering connection, etc.)

Route tables are needed to make a subnet public because they define where traffic is sent, and a subnet is only considered public if its route table includes a route that directs internet-bound traffic (0.0.0.0/0) to an Internet Gateway.

Without this route, resources in the subnet cannot reach or be reached from the internet, even if they have public IP addresses.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-security_0a07b191)

---

## Route destination and target

Routes are defined by their destination and target, which mean:

Destination is the IP address range (CIDR block) that determines which traffic the rule applies to (for example, 0.0.0.0/0 for all internet traffic).

Target is the network component to which traffic matching the destination is sent (such as an Internet Gateway, NAT Gateway, or another VPC).

The route in my route table that directed internet-bound traffic to my internet gateway had a destination of 0.0.0.0/0 and a target of igw-0be04cb691ae174ac

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-security_0a07b191)

---

## Security groups

Security groups are virtual firewalls in AWS that control inbound and outbound traffic for resources such as EC2 instances within a VPC.

What security groups do

Security groups:

Allow or deny traffic based on rules.
Control traffic using protocol, port number, and source/destination.
Are stateful (if inbound traffic is allowed, the response is automatically allowed)

Key characteristics:

Operate at the instance level
Support allow rules only (no explicit deny)
Can be attached to multiple resources
Rules can reference other security groups

### Inbound vs Outbound rules

Inbound rules are security group rules that define which incoming traffic is allowed to reach a resource, based on the protocol, port number, and source IP address or security group.
I configured an inbound rule that includes the IPv4 version, Type HTTP, Protocol TCP, Port range 80, and source 0.0.0.0/0

Outbound rules are security group rules that define which traffic is allowed to leave a resource, specifying the destination, protocol, and port.

By default, my security group's outbound rule allows all outbound traffic to any destination (0.0.0.0/0), meaning the resource can initiate connections to the internet or other services unless restricted.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-security_92b0b0b4)

---

## Network ACLs

Network ACLs (NACLs) are optional, stateless firewalls that control inbound and outbound traffic at the subnet level in a VPC.

What NACLs do:

Allow or deny traffic based on rules for IP ranges, protocols, and ports.

Apply to all resources in the associated subnet.

Are stateless (responses to allowed inbound traffic are not automatically allowed outbound—you must create a corresponding rule).

Can have allow and deny rules, unlike security groups, which only allow.

### Security groups vs. network ACLs

The difference between a security group and a network ACL is that a security group acts as a stateful firewall at the instance level, allowing only specified inbound and outbound traffic, while a network ACL is a stateless firewall at the subnet level that can allow or deny traffic and requires separate rules for inbound and outbound responses.

---

## Default vs Custom Network ACLs

### Similar to security groups, network ACLs use inbound and outbound rules

By default, a network ACL's inbound and outbound rules will allow all traffic.

This means that unless you add custom rules, all incoming and outgoing traffic to the subnet is permitted.

By default, a network ACL's inbound and outbound rules will allow all traffic.

This means that unless you add custom rules, all incoming and outgoing traffic to the subnet is permitted.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-security_4faeb056)

---

## Tracking VPC Resources

---

---
