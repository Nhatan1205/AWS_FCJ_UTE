# Day 19: VPC Peering

## Lab 19-01: Set Up VPC Peering (Introduction)

By default, **VPCs (Virtual Private Clouds)** are isolated from each other and cannot communicate directly. However, **VPC peering** is a networking connection between two VPCs that enables instances in either VPC to communicate with each other using **private IP addresses** — **without going through the public internet**. This enhances **security**, **performance**, and **cost-efficiency**.  
> **Note:** Each VPC can have up to **50 active VPC peering connections** by default (soft limit, can be increased via AWS support).

---

## Important Concepts Before the Lab

- **Cross-VPC DNS Resolution (Cross-Peering DNS)**  
  This feature allows resources in one VPC to resolve **DNS names of private resources in the peer VPC**.  
  _Example: Resolving private DNS of an EC2 instance in the peer VPC._

- **Network ACLs (Access Control Lists)**  
  Stateless firewalls applied at the **subnet level**.  
  Unlike security groups, **NACLs** must allow both **inbound and outbound** rules because they do not track connection state.

---

## Pre-requisites

- Two VPCs must be configured with **non-overlapping CIDR blocks**  
  _Example: VPC A: `10.0.0.0/16`, VPC B: `192.168.0.0/16`_
- Appropriate IAM permissions to create/accept peering connections and update route tables.

---

## Steps to Set Up VPC Peering

1. **Open the VPC Dashboard** in the AWS Management Console.

2. **Navigate to "Peering Connections"**  
   - This section allows you to create and manage peering links between two VPCs.
   - Peering allows routing traffic via **private IPv4/IPv6 addresses**.

3. **Create a Peering Connection**
   - Choose the **Requester VPC** (initiator).
   - Select the **Accepter VPC** (can be in the same or a different AWS account or region).
   - Add name tags for easier identification.

4. **Accept the Peering Request**
   - Go to the Accepter side.
   - Accept the **pending peering request**.

5. **Update Route Tables in Both VPCs**
   - In each VPC, update the route table.
   - Add a route that sends traffic to the peer VPC's CIDR block via the peering connection.

6. **(Optional) Enable DNS Resolution**
   - Edit the peering connection to allow **DNS resolution from remote VPC**.

7. **Verify Network ACLs and Security Groups**
   - Ensure **NACLs and security groups** allow the desired traffic (e.g., SSH, HTTP).

---

Let me know if you want a diagram or a step-by-step AWS Console guide!
