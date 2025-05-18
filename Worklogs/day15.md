# Day 15: Comprehensive Review of VPC

---

## VPC Overview

A **Virtual Private Cloud (VPC)** allows you to provision a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network you define.

**Key features:**
- Control over IP address range
- Creation of subnets
- Configuration of route tables and gateways
- Multiple layers of security

When creating a VPC, you must assign an **IPv4 CIDR block** (between `/16` and `/28`). Once set, this block **cannot be changed**. Each subnet you create within the VPC must also have its own CIDR block.

---

## Subnets

A **subnet** is a segment within your VPC used to group and isolate resources. Subnets can be either:
- **Public**: connected to the internet
- **Private**: isolated from direct internet access

Each subnet can support **up to 251 usable IP addresses** (from a /24 block).

---

## Elastic IP (EIP)

When an EC2 instance is stopped and started, its public IP changes. This causes issues with DNS and firewall configurations.

**Elastic IP** solves this by:
- Assigning a static public IP address to an instance
- Allowing the IP to be re-associated with another instance in the same region
- Simplifying DNS and firewall rule management

---

## Route Tables

A **route table** contains rules (routes) that determine how network traffic is directed.

**Each route includes:**
- **Destination**: IP address or subnet to route traffic to
- **Target**: AWS resource (e.g., internet gateway, NAT gateway)

**Important:**
- Every subnet must be associated with a route table
- A subnet can only be associated with one route table at a time
- One route table can be associated with multiple subnets
- Default route: `local` (for intra-VPC communication)

---

## Internet Gateway

An **internet gateway** is used to enable communication between instances in your VPC and the internet.

**Functions:**
1. Provides a target for internet-bound traffic in route tables
2. Performs NAT for instances with public IPv4 addresses

Used primarily with public subnets.

---

## Network ACL (NACL)

A **Network Access Control List** is a set of rules that control inbound and outbound traffic at the subnet level.

**Key points:**
- Operates at the network level
- Supports both **allow** and **deny** rules
- Adds a layer of security in addition to security groups
- Useful when you have many instances in a subnet and need centralized control (like a firewall)

---

## NAT Gateway

A **NAT Gateway** enables instances in a private subnet to access the internet (for software updates, API calls, etc.), while preventing inbound internet access.

**How it works:**
- EC2 in private subnet sends a request to NAT Gateway
- NAT Gateway forwards request to the internet
- Internet sends response to NAT Gateway → NAT Gateway forwards it to EC2

**Advantages:**
- Keeps private instances secure
- Avoids assigning public IPs

---

## VPC Peering

A **VPC peering connection** allows you to route traffic between two VPCs privately.

**Important notes:**
- Traffic is routed using route tables
- VPCs must be in the same region or supported inter-region combinations
- No transitive peering (each VPC must peer with every other directly)

---

## VPC Endpoint

A **VPC endpoint** allows private connections to AWS services (e.g., S3, DynamoDB) without using:
- Internet Gateway
- NAT Gateway
- VPN

**Benefits:**
- Reduced NAT Gateway costs
- Avoids routing traffic over the public internet
- Improves security for accessing AWS services

---

## Security Group

A **security group** acts as a virtual firewall for EC2 instances.

**Key points:**
- Controls **inbound and outbound** traffic
- Applied at the **instance level**
- Stateful: return traffic is automatically allowed
- Rules define what traffic is allowed (no deny rules)

---

## Transit Gateway

A **Transit Gateway** acts as a central hub to connect:
- Multiple VPCs
- On-premises data centers
- Other AWS services (Direct Connect, Site-to-Site VPN)

**Why use it?**
- Simplifies network architecture
- Avoids creating complex VPC peering meshes

Example: Connecting 10 VPCs directly would need 45 peering connections; with a Transit Gateway, you need only 10.

---

## Route 53

**Amazon Route 53** is a powerful Domain Name System (DNS) service that helps route end-user requests to your application.

**Capabilities:**
- Domain registration and management (e.g., `mywebsite.com`)
- DNS routing to AWS services like EC2, S3, CloudFront
- Health checks for failover
- Smart load balancing (Latency-Based Routing, Geo Routing)

---

## Amazon CloudFront

**Amazon CloudFront** is AWS’s Content Delivery Network (CDN) service.

**Purpose:**
- Distribute content (images, videos, files) to users faster
- Stores content in **edge locations** (servers around the world)
- Reduces latency by serving content from the location closest to the user

**Use Cases:**
- Accelerate website performance
- Reduce load on origin servers
- Provide secure content delivery
