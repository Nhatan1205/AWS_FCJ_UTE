# Day 10: Practice with VPC – Lab 3 (continued)

## Lab03-02.3 – VPC Resource Map

### Create VPC
1. Go to **VPC** service in AWS Console.
2. Click **Create VPC**.
3. Select **VPC only** option.
4. Add a **Name tag** (for easier identification).
5. Input **IPv4 CIDR block** (e.g., `10.10.0.0/16`, must be between `/16` and `/28`).
6. Select **No IPv6 CIDR block**.
7. Set **Tenancy** to `default`.
8. Click **Create VPC`.

> Once created, resources such as subnets, route tables, and network connections will be visible.

---

## Lab03-03.1 – Create VPC (repeat of above)

Follow the same steps as in Lab03-02.3.

---

## Lab03-03.2 – Create Subnets

### Public Subnet 1
- Go to **Subnets**
- Select your **VPC**
- Set:
  - Name: `Public Subnet 1`
  - Availability Zone: e.g., `ap-southeast-1a`
  - CIDR Block: `10.10.1.0/24`
- Click **Create Subnet**

### Other Subnets
- **Public Subnet 2**: `10.10.2.0/24`
- **Private Subnet 1**: `10.10.3.0/24`
- **Private Subnet 2**: `10.10.4.0/24`

### Enable Auto-Assign Public IP
- Go to **Subnet**
- Click **Actions** → **Edit subnet settings**
- Tick **Enable auto-assign public IPv4 address**

> This step distinguishes public from private subnets.

---

## Lab03-03.3 – Create Internet Gateway

1. Go to **Internet Gateways**
2. Click **Create Internet Gateway**
3. Add a **Name tag** and click **Create**
4. Click **Attach to VPC**, choose your VPC

---

## Lab03-03.4 – Route Table for Outbound Internet

1. Go to **Route Tables**
2. Click **Create Route Table**
3. Add a **Name tag**, select your **VPC**, click **Create**
4. Click **Edit routes**, add:
   - **Destination**: `0.0.0.0/0`
   - **Target**: Your Internet Gateway
5. Click **Subnet associations** → **Edit subnet associations**
6. Select your **Public Subnets**

> One route table can be linked to multiple subnets.

---

## Lab03-03.5 – Create Security Groups

### Public Subnet Security Group
1. Go to **Security Groups** → **Create**
2. Add:
   - Name: `MyPublicSecurity`
   - Description
   - VPC: your created VPC
3. Add **Inbound Rules**:
   - **Type**: SSH — Source: `My IP`
   - **Type**: All ICMP - IPv4 — Source: `0.0.0.0/0`

### Private Subnet Security Group
- Same process, but:
  - **SSH source** should be the **security group ID of Public Subnet** (MyPublicSecurity)

---

## ✅ Summary Table

| Component            | Details                                                                 |
|---------------------|-------------------------------------------------------------------------|
| VPC                 | `10.10.0.0/16`, no IPv6                                                 |
| Subnets             | Public: `10.10.1.0/24`, `10.10.2.0/24`<br>Private: `10.10.3.0/24`, `10.10.4.0/24` |
| Internet Gateway    | Created and attached to VPC                                             |
| Route Table         | Route `0.0.0.0/0` to IGW, associated with public subnets                 |
| Security Groups     | Public: SSH from My IP, ICMP all<br>Private: SSH from Public SG         |
