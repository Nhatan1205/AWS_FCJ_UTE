# Lab 03-01: Start with Amazon VPC and AWS VPN Site-to-Site

## 1. VPC Overview

VPC (Virtual Private Cloud) is a dedicated and isolated network within AWS that enables you to run resources like EC2 instances, databases, and other services. It is separated from the public internet and other AWS customers' environments, providing full control over networking configurations.

- **VPC Configuration:**
   - You can define your VPC's CIDR (Classless Inter-Domain Routing) block, typically an IPv4 address range such as `10.0.0.0/16`.
   - This CIDR block can be split into subnets to allocate address space to different areas of the VPC.
   - **Private and Public Subnets:** A VPC typically contains private and public subnets that manage traffic based on specific access requirements.
   - **Internet Gateway (IGW):** For resources within the VPC to access the internet, you must attach an Internet Gateway to the VPC.

## 2. Lab 03-01.1: Subnets

A subnet is a smaller segment of your VPC's CIDR block. It enables you to isolate and organize resources within the VPC.

- **CIDR and Subnet:** Subnets must fit within the VPC’s CIDR range. For instance, if your VPC’s CIDR is `10.0.0.0/16`, a subnet could be `10.0.1.0/24`.
- **Subnet Types:**
   - **Private Subnet:** Resources in this subnet do not have direct internet access.
   - **Public Subnet:** Resources here can access the internet through an Internet Gateway.
- **Subnet Size:** The smallest subnet you can create is a `/28`, offering 16 IP addresses.
- **Auto-Assign Public IP:** When launching instances in a public subnet, you can enable automatic assignment of public IPs, allowing direct access from the internet.

## 3. Lab 03-01.2: Route Table

Route tables determine how traffic is routed within a VPC.

- **Routing in Subnets:** A subnet’s route table defines how traffic is directed within and outside the subnet.
- **Default Route Table:** Every VPC comes with a default route table, which routes internal traffic within the VPC. You cannot delete this default route table.
- **Custom Route Tables:** You can create custom route tables to manage traffic flow between subnets or to the internet, for example, directing traffic from a private subnet to a NAT gateway for internet access.

## 4. Lab 03-01.3: Internet Gateway (IGW)

An Internet Gateway is a component that allows VPC resources to access the internet.

- **Role of IGW:** It acts as a translator between private IPs within the VPC and public IPs, enabling outbound internet access and inbound communication.
- **High Availability:** IGWs are designed to scale automatically with the VPC, ensuring reliability.
- **Function:** When an EC2 instance in a public subnet receives traffic from the internet, the IGW translates its public IP to the private IP assigned to the EC2 instance.

