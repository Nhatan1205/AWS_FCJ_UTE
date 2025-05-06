# Day 07: VPC (cont) + Load Balancer

## VPC Security and Multi-VPC Features

### Security Group:
A **Security Group** acts as a virtual firewall to control the inbound and outbound traffic to your AWS resources. It is stateful, meaning it tracks the connection state and only allows traffic that is part of an established connection.

- **Rules** are restricted by protocol, source address, port, or another security group.
- Security group rules can only be **allow** rules (no deny rules).
- It is applied to **Elastic Network Interfaces (ENIs)**, which are associated with EC2 instances.

By default, a security group blocks all incoming traffic but allows all outgoing traffic. Therefore, you need to modify the **Inbound** rules to define what traffic can enter, and update the **Outbound** rules as needed.

You can assign multiple security groups for different purposes. For example, if you have two EC2 instances in a subnet—a **Webserver** and a **Database**—you could use different security groups for each, depending on the security requirements.

### Network Access Control List (NACL):
A **NACL** is a stateless firewall that controls traffic going in and out of an AWS resource, applied at the **subnet** level.

- NACL rules are restricted by protocol, source address, and port.
- NACLs must explicitly define both **inbound and outbound** rules since they do not maintain state.
- By default, NACL allows all inbound and outbound traffic, but you can restrict this by creating custom rules.
- Rules are processed in the **numerical order**: the first rule that matches is applied.

NACLs affect all resources within a subnet. For example, if one subnet is configured to block traffic from certain IPs, it will apply to all instances in that subnet.

### VPC Flow Logs:
**VPC Flow Logs** capture information about IP traffic going to and from network interfaces in your VPC. These logs can be published to **Amazon CloudWatch Logs** or **Amazon S3** for further analysis.

- Flow logs **do not capture** the content of packet data but can help identify abnormal traffic patterns.
- This feature is useful for troubleshooting, monitoring network traffic, and enhancing security by detecting unusual activities.
- For example, flow logs can be used in combination with other security tools to detect and mitigate potential threats.

---

## VPC Peering and Transit Gateway:

### VPC Peering:
**VPC Peering** enables you to connect two or more VPCs so that resources in those VPCs can communicate directly without going through the internet. This improves security by keeping internal traffic private.

- Peering is a **1:1 connection** between two VPCs and **does not support transitive routing**. This means you cannot route traffic between VPC A and VPC B through a third VPC (C).
- If VPCs have overlapping IP address ranges, peering will not work.

However, managing multiple peering connections can become complex if you have many VPCs, as you would need to establish a peering connection between each pair of VPCs.

### Transit Gateway:
The **Transit Gateway (TGW)** provides a scalable and centralized solution for connecting multiple VPCs and on-premises networks. It simplifies network management and avoids the complexity of managing numerous VPC peering connections.

- Transit Gateways work at the **availability zone (AZ)** level.
- You can attach subnets from various VPCs to the TGW. Once attached, all subnets connected to the TGW can communicate with each other.
- Transit Gateways are ideal for large-scale network setups, where you need to connect multiple VPCs efficiently.

---

## VPN - Direct Connect - Load Balancer - Extra Resources:

### VPN Site-to-Site:
A **Site-to-Site VPN** connects a traditional on-premises data center to your AWS VPC in a **hybrid architecture**. It uses **two endpoints**: one on the AWS side (Virtual Private Gateway) and one on the customer’s side (Customer Gateway).

- The connection is persistent and provides secure communication between your on-premises data center and AWS.

### VPN Client-to-Site:
A **Client-to-Site VPN** allows an individual host (for example, an employee’s laptop) to securely connect to the AWS VPC. 

- This is ideal for remote access and is **recommended** for accessing AWS resources from external devices.

### AWS Direct Connect:
**AWS Direct Connect** provides a private, dedicated network connection between your data center and AWS. It offers lower latency compared to standard internet connections.

- It is especially useful for high-performance applications that require stable and low-latency connections.
- **Direct Connect** operates in Vietnam through **AWS Direct Connect Partners**, providing hosted connections.
- Typical latency is around **20-30 ms**.

---

## Elastic Load Balancing (ELB):
**Elastic Load Balancing (ELB)** automatically distributes incoming application traffic across multiple targets, such as EC2 instances, containers, and IP addresses, within one or more availability zones.

- It supports various protocols, including **HTTP**, **HTTPS**, **TCP**, and **SSL**.
- ELBs can be used in both **public** and **private** environments.
- Each ELB is assigned a **DNS name** and traffic is routed through DNS.
- The **Network Load Balancer** supports static IP addresses, whereas other types rely on dynamic IPs.
- There are **four types** of ELBs:
  1. **Application Load Balancer (ALB)**: Best for HTTP and HTTPS traffic.
  2. **Network Load Balancer (NLB)**: Ideal for high-performance and TCP/SSL traffic.
  3. **Classic Load Balancer (CLB)**: An older model supporting both HTTP and TCP traffic.
  4. **Gateway Load Balancer (GLB)**: Used for integrating with third-party virtual appliances such as firewalls.

---
