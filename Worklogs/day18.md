# Day 18: Practice with Route 53 (Part 2)

---

## Lab 10-05.2 – Create Route 53 Resolver Rules

In this lab, you’ll create a **Route 53 Resolver rule** of type **Forward**, which allows DNS queries for a specific domain (e.g., `onprem.example.com`) to be forwarded to an external DNS resolver, such as an on-premises Active Directory DNS server.

### Types of Rules

- **Forward** – Forwards DNS queries for a specific domain to a custom DNS server (e.g., on-premises).
- **System** – Internal AWS DNS rules used to resolve standard domains (e.g., for internet-based queries).

### Steps to Create a Forwarding Rule

1. Go to the **Route 53** service in the AWS Console.  
   Under the **Resolver** section in the left menu, click **Rules**.  
   You should see a default system rule (used for resolving internet queries).

2. Click **Create rule**.

3. Fill in the following details:
   - **Name**: `ForwardToOnPremAD`
   - **Rule type**: `Forward`
   - **Domain name**: `onprem.example.com.`
   - **VPC that uses this rule**: `HybridDNS-VPCStack`
   - **Outbound endpoint**: `R53-OutboundEndpoint`

4. Under **Target IP addresses**:
   - Add the two IP addresses listed under the **DNS Address** of your AWS Managed Directory Service.
   - These addresses are on **port 53**.

5. Click **Submit** to create the rule.

✅ You have now created a **Route 53 Resolver forwarding rule** that directs queries for `onprem.example.com` to your on-prem DNS (e.g., AWS Managed Microsoft AD).

---

## Lab 10-05.3 – Create Route 53 Inbound Endpoints

An **inbound endpoint** allows DNS queries from your on-premises environment (or external DNS servers) to be resolved **by Route 53** for hosted zones managed in AWS.

### Steps to Create an Inbound Endpoint

1. In the Route 53 Console, under **Resolver**, select **Inbound endpoints**.

2. Click **Create inbound endpoint**.

3. Fill in the following information:
   - **Endpoint name**: `R53-InboundEndpoint`
   - **VPC**: `HybridDNS-VPCStack`
   - **Security group**: `d-###...#_controllers` (created by CloudFormation)
   - **Endpoint type**: `IPv4`

4. Add IP addresses for the inbound endpoint:
   - Choose two **Availability Zones (AZs)**.
   - Select **private subnets** in each AZ.
   - Leave the **IPv4 addresses** to be auto-assigned.

5. Click **Create**.

✅ AWS will provision two **Elastic Network Interfaces (ENIs)** that serve as entry points for DNS queries from outside the VPC.

---

## Lab 10-05.4 – Test Results

After setup, verify that DNS resolution is working:

### Using Command Prompt
```cmd
nslookup onprem.example.com
```

## Deploy AWS Managed Directory Service

### Steps to Deploy

1. Go to the **Directory Service** in the AWS Console.

2. Click **Set up directory**.

3. Select **AWS Managed Microsoft AD** and click **Next**.

4. Choose **Standard Edition**.  
   Enter:
   - **Directory DNS Name**: `onprem.example.com`

5. Enter an **Admin password**, then click **Next**.

6. Choose the **Hybrid VPC**.  
   Select **two private subnets** in different Availability Zones (AZs).  
   Click **Next**, then **Create directory**.

> ⏳ **Note:** It may take **10–20 minutes** to fully create the directory.

---

### After Directory Creation

- Navigate to the **directory details** page.
- You will see **two DNS IP addresses** listed under the **Networking** section.
- These IPs correspond to **Elastic Network Interfaces (ENIs)** attached to the AD Domain Controllers.
- Use these IP addresses when configuring **Route 53 Resolver forwarding rules**.
