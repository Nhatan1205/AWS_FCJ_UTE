# Day 20: Practice VPC Peering

## Lab 19-02.1 - Initialize CloudFormation Templates

We will use AWS **Application Composer** to visually build VPC infrastructure or upload CloudFormation templates directly from local files.

### Step-by-step:

1. **Download the Template:**
   - Download the CloudFormation template using one of the provided links (`Link_template_file` or `Link_download_template`).

2. **Upload and Deploy First VPC:**
   - Go to **CloudFormation > Create stack**.
   - Choose **Upload a template file** and select the downloaded template.
   - Stack Name: `My-VPC-Stack`
   - Environment Name Parameter: `My VPC`
   - IP Range: Use unique CIDR blocks that will not conflict with the second VPC.
   - Click **Next**, then **Submit** to deploy.

3. **Deploy Second VPC (HG VPC):**
   - Stack Name: `HG-VPC-Stack`
   - Use the following parameters:
     - `EnvironmentName`: `HG VPC`
     - `VpcCIDR`: `10.10.0.0/16`
     - `PrivateSubnet1CIDR`: `10.10.3.0/24`
     - `PrivateSubnet2CIDR`: `10.10.4.0/24`
     - `PublicSubnet1CIDR`: `10.10.1.0/24`
     - `PublicSubnet2CIDR`: `10.10.2.0/24`
   - Click **Next** and **Submit**

Result: The VPC architecture created should closely resemble the provided reference architecture.

---

## Lab 19-02.2 - Create Security Groups

To enable ICMP traffic (ping) between EC2 instances in both VPCs, we need to configure security groups accordingly.

### Create Security Group for `My VPC`:

- Name: `MY VPC SG`
- Description: Security group for My VPC EC2 instances
- VPC: Select `My VPC`
- Inbound Rules:
  - Type: `SSH` | Source: `My IP`
  - Type: `All ICMP - IPv4` | Source: `Anywhere`
  - Type: `All ICMP - IPv4` | Source: `10.10.0.0/16` (CIDR of HG VPC)

### Create Security Group for `HG VPC`:

- Name: `HG VPC SG`
- Description: Security group for HG VPC EC2 instances
- VPC: Select `HG VPC`
- Inbound Rules:
  - Type: `SSH` | Source: `My IP`
  - Type: `All ICMP - IPv4` | Source: `Anywhere`
  - Type: `All ICMP - IPv4` | Source: `172.31.0.0/16` (CIDR of My VPC)

---

## Lab 19-02.3 - Launch EC2 Instances

Create EC2 instances in the public subnets of both VPCs for testing connectivity.

### Launch EC2 in My VPC:

- Name: `EC2 - My VPC`
- AMI: Amazon Linux 2 (HVM), SSD Volume Type
- Instance Type: `t2.micro`
- Key Pair: Create or select `vpcpeering-key` (RSA format, `.pem`)
- Network: `My VPC`
- Subnet: `My VPC Public Subnet (AZ2)`
- Auto-assign Public IP: Enabled
- Security Group: `MY VPC SG`

### Launch EC2 in HG VPC:

- Name: `EC2 - HG VPC`
- VPC: `HG VPC`
- Subnet: `HG VPC Public Subnet (AZ2)`
- Auto-assign Public IP: Enabled
- Security Group: `HG VPC SG`

### Connect Using MobaXterm:

1. Start a new SSH session.
2. Remote host: Public IPv4 of EC2 instance
3. Username: `ec2-user` (or `ubuntu` if using Ubuntu AMI)
4. Use the private key file downloaded earlier (.pem)

### Ping Test:

- From EC2 in My VPC: `ping amazon.com -c5`
- From EC2 in HG VPC: `ping amazon.com -c5`
- Try pinging the other EC2 instance's private IP:
  - `ping <Private IP of HG VPC EC2>`
  - At this point, ping will fail because routing is not yet set up.

---

## Lab 19-03 - Update Network ACLs (NACLs)

To allow pinging between private subnets, we must update the Network ACLs.

### Steps:

1. Go to **VPC > Network ACLs**.
2. Select the NACL associated with HG VPC.
3. Edit the **inbound rules**:
   - Allow traffic from `172.31.0.0/16` (CIDR of My VPC)
   - Set rule number (e.g., 110), allow `All Traffic` from that CIDR block.

Note: This may also block ping from the internet, depending on rule configuration.

---

## Lab 19-04 - Create a VPC Peering Connection

Now create the VPC peering connection to enable communication between the two VPCs.

### Steps:

1. Go to **VPC > Peering Connections**.
2. Click **Create Peering Connection**.
3. Set the following:
   - Name tag: `lab-vpc-peer`
   - VPC (Requester): `My VPC`
   - Account: `My account` (both VPCs are in the same AWS account)
   - Region: `This region (ap-southeast-1)`
   - VPC (Accepter): `HG VPC`
4. Click **Create Peering Connection**

### Accept Peering Request:

- In the Peering Connection list, find the pending request.
- Click **Actions > Accept Request**
- Status should change to **Active**

If you try pinging EC2-HG’s private IP from EC2-MyVPC now, it will still fail because route tables have not been updated.
