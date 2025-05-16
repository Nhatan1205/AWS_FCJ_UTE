# Day 13: Practice – EC2 Instance Connect Endpoint, Route 53, and Key Pair

## Lab03-04.5 – EC2 Instance Connect Endpoint

### Goal:
Securely and cost-effectively connect to a private EC2 instance without requiring a public IP address, using EC2 Instance Connect Endpoint over SSH or RDP.

### Why this matters:
Connecting directly to a private EC2 instance via public IP exposes it to the internet and adds cost. Using EC2 Instance Connect Endpoint keeps it private and secure.

### Steps:

1. Go to **VPC** service in AWS Console.
2. Create a **Security Group** (e.g., name it `Endpoint_SG`)  
   - **Inbound rules:** Allow SSH (port 22) from **My IP**.
3. Navigate to **Endpoints** section in the VPC console.
4. Click **Create Endpoint**.
5. Fill in the required information:
   - **Name:** `EC2-private-endpoint`
   - **Category:** EC2 Instance Connect Endpoint
   - **Select VPC** and **Private Subnet**
   - Attach the **Endpoint_SG** security group
6. Connect to the private EC2 instance:
   - Go to **EC2 > Instances**
   - Select your **private instance**
   - Click **Connect** > **EC2 Instance Connect Endpoint** tab > **Connect**
7. If connection fails:  
   - You likely forgot to add a **security group rule** that allows traffic from the **Endpoint’s security group to the EC2’s security group**:
     - Example rule: In the **private EC2’s security group**, allow SSH from **Custom: sg-08f… (the endpoint’s SG)**.

### Result:
Successfully accessed private EC2 instance via EC2 Instance Connect Endpoint without exposing it to the internet.

---

## Lab10-01 – Set Up Hybrid DNS with Route 53 Resolver

### Goal:
Integrate AWS DNS (Route 53) with an on-premises DNS system using Route 53 Resolver to enable hybrid DNS resolution.

### Why this matters:
In hybrid cloud environments, it’s important for AWS resources to resolve on-premises domain names, and vice versa.

### Key Concepts:

- **Route 53:** AWS’s scalable DNS service. Can register and manage domain names.
- **Inbound Endpoint:** Accepts DNS queries from on-premises to AWS-hosted domain names.
- **Outbound Endpoint:** Sends DNS queries from AWS to on-premises DNS servers.
- **Rules:** Define conditions for which domain names AWS should forward to your on-prem DNS system.

### Result:
Created Route 53 Resolver endpoints and DNS forwarding rules to enable name resolution across on-premises and AWS.

---

## Lab10-02.1 – Generate Key Pair

### Goal:
Create a secure key pair for accessing EC2 instances (especially Windows instances using RDP).

### Why this matters:
AWS uses public-key cryptography to secure instance access. The private key stays with you, and AWS uses the public key to verify access.

### Steps:

1. Go to the **EC2** service.
2. In the **Key Pairs** section, click **Create Key Pair**.
3. Fill in:
   - **Name:** e.g., `hybrid-DNS`
   - **Key type:** RSA
   - **Private key format:** `.pem` (for Linux/Mac) or `.ppk` (for PuTTY on Windows)
   - **Tag:** Add a name tag for organization
4. Save the private key file (`.pem`) securely on your machine.
   - Required when connecting to EC2 via SSH or RDP.

### Result:
Generated a secure key pair that allows safe, encrypted access to your EC2 instances.

---

## Goal Summary:

- Understand how to securely access EC2 in private subnets using Instance Connect Endpoints  
- Learn to set up hybrid DNS using Route 53 Resolver endpoints  
- Create and manage key pairs for secure EC2 instance access
