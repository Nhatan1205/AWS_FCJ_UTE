# Day 13: Practice with EC2 Instance Connect Endpoint, Route 53, and Key Pair Management

---

## Lab03-04.5 - EC2 Instance Connect Endpoint

To securely and cost-effectively access private EC2 instances without assigning them public IP addresses, AWS provides the **EC2 Instance Connect Endpoint**. This allows SSH (for Linux) and RDP (for Windows) access through the VPC, enhancing both security and network isolation.

### Steps:

**Step 1:** Navigate to the **VPC** service in the AWS Console.

**Step 2:** Create a **Security Group** specifically for the EC2 Instance Connect Endpoint.
- Name: `Endpoint_SG`
- Inbound Rules:  
  - Type: SSH  
  - Source: My IP (to restrict access only from your current IP address)

**Step 3:** In the VPC dashboard, go to the **Endpoints** section.

**Step 4:** Click **Create Endpoint**.

**Step 5:** Configure the Endpoint:
- Name: `EC2-private-endpoint`
- Service Category: EC2 Instance Connect Endpoint
- VPC: Select your existing VPC
- Security Group: Choose the `Endpoint_SG` created in Step 2
- Subnets: Select a **private subnet** (one that has no direct route to the internet)

**Step 6:** Connect to a private EC2 instance using the EC2 Instance Connect Endpoint:
- Go to EC2 → Instances
- Select your **private EC2 instance**
- Click the **Connect** button
- Select the tab: **EC2 Instance Connect Endpoint**
- Click **Connect**

**Note:** If you encounter a connection error at this step, it's likely because the security group associated with the private EC2 instance does not allow inbound SSH connections from the security group assigned to the endpoint.

**Fix:**
- Go to the Security Group assigned to your **private EC2 instance**
- Add an **inbound rule**:
  - Type: SSH
  - Source: Custom — select the security group ID of `Endpoint_SG` (e.g., `sg-08f...`)

---

## Lab10-01 - Set up Hybrid DNS with Route 53 Resolver

Amazon Route 53 is AWS’s scalable and highly available DNS (Domain Name System) web service. You can configure hybrid DNS with Route 53 Resolver to integrate your on-premises DNS infrastructure with AWS, allowing for seamless name resolution between the two environments.

### Key Components:

- **Route 53 Domain Registration:**  
  - You can register a new domain name directly in Route 53.  
  - Enter your desired domain name, and click **Check** to verify its availability.

- **Inbound Endpoint:**  
  - Acts as the target for on-premises DNS queries that resolve to AWS-hosted domain names.

- **Outbound Endpoint:**  
  - Forwards DNS queries originating from AWS resources to your on-premises DNS servers.

- **Rules:**  
  - Define DNS forwarding policies that specify which domain queries should be forwarded to specific DNS endpoints (e.g., on-premises DNS servers).

Hybrid DNS setups are essential for organizations adopting a hybrid cloud strategy, enabling integrated name resolution between AWS and on-prem environments.

---

## Lab10-02.1 - Generate Key Pair for EC2 Access

AWS allows you to securely access your EC2 instances using public-private key pairs. The public key is stored by AWS and injected into the EC2 instance, while the private key is downloaded and stored by the user. This mechanism is used for secure SSH (Linux) or RDP (Windows) access.

### Use Case:

You will create a key pair for use with Windows EC2 instances, enabling secure access via Remote Desktop (RDP).

### Steps:

**Step 1:** Open the **EC2** service in the AWS Management Console.

**Step 2:** Navigate to the **Key Pairs** section under **Network & Security**.

**Step 3:** Click **Create Key Pair**.

**Step 4:** Fill in the required information:
- Name: `hybrid-DNS`
- Key Type: RSA
- Private Key Format: `.pem` (used for Linux/Mac and required for later conversion to `.ppk` for Windows access)
- Tags: (Optional) Add a name tag such as `Name=hybrid-DNS`

**Important:** Download and safely store the `.pem` file on your local machine — it cannot be retrieved later from AWS.

You can later convert this `.pem` to `.ppk` using PuTTYgen if you're accessing the instance from a Windows environment with PuTTY.
