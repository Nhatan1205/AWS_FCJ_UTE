# Day 17: Practice DNS with Route 53

## Lab10-05: Set Up DNS with Route 53

**Amazon Route 53** is a scalable and highly available Domain Name System (DNS) web service. It is primarily used for:

- Domain registration  
- DNS routing  
- Health checking of resources

In this lab, we focus on **DNS resolution** using **Route 53 Resolver**, which facilitates DNS query handling between your **Amazon VPC (Virtual Private Cloud)** and **external networks**, such as your on-premises environment.

---

## Understanding Route 53 Resolver

The Route 53 Resolver enables DNS query routing through **Inbound** and **Outbound Endpoints**:

- **Outbound Endpoint**:  
  Allows DNS queries originating from your AWS resources (e.g., EC2 instances) inside a VPC to be forwarded to DNS servers **outside of AWS**, such as an **on-premises Active Directory** or an external DNS service.

- **Inbound Endpoint**:  
  Allows external DNS queries (e.g., from your on-premises Active Directory or DNS infrastructure) to **enter AWS** and resolve domain names hosted within your AWS environment (such as private hosted zones in Route 53).

- When using DNS inside a VPC, AWS automatically assigns a default DNS resolver IP to your EC2 instances, typically **VPC CIDR base IP + 2**.  
  For example:  
  If your VPC CIDR is `10.0.0.0/16`, the DNS resolver IP is `10.0.0.2`.

- Route 53 can forward queries to AWS services like **EC2, RDS, S3**, etc., depending on your DNS forwarding rules.

- In traditional (non-AWS) environments, you would manually configure the DNS server IP addresses. Route 53 helps automate and simplify this process within AWS.

---

## Lab10-05.1: Create a Route 53 Outbound Endpoint

The goal of this lab is to **create a Route 53 Resolver Outbound Endpoint** that allows DNS queries from your AWS VPC to be **forwarded to external DNS servers** (e.g., an on-premises DNS service).

### Step-by-Step Instructions

#### Step 1: 
- Navigate to the **Route 53** service in the AWS Management Console.
- Go to the **Resolver** section and select **Outbound Endpoints**.
- Click **"Create Outbound Endpoint"**.

#### Step 2: General Settings
- **Endpoint name**: `R53-OutboundEndpoint`
- **VPC**: Select the VPC where this resolver will be used (e.g., `HybridDNS-VPCStack-...`)
- **Security group**: Choose a security group that allows outbound DNS traffic (usually port 53 UDP/TCP)

#### Step 3: IP Addresses
You need to provide two IP addresses located in **different Availability Zones (AZs)** to ensure high availability:

- For each IP, select:
  - **Availability Zone** (AZ)
  - **Private Subnet** in that AZ
  - Leave **IPv4 address** blank to let AWS auto-assign

#### Step 4: Protocol Settings
- **Protocol**: `Do53` (DNS over port 53)
- **IP Version**: `IPv4`

#### Step 5: Tags
Add a tag to help organize and manage this resource:
- **Key**: `Outbound`
- **Value**: `R53`

#### Step 6:
- Click **"Create"** to launch the Outbound Resolver Endpoint.

---

## Result

After creation, the Outbound Resolver Endpoint will have **two network interfaces assigned** in private subnets across different AZs.  
These interfaces will receive IPs managed by AWS, which your VPC-based applications (like EC2) can use to forward DNS queries to external destinations.


