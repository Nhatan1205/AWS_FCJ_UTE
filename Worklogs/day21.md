# Day 21: Route Tables and Cross-Peer DNS

## Lab 19-05 - Configure Route Tables

To enable traffic routing between the two VPCs, we need to update their respective route tables.

### Update My VPC Route Table

1. Go to **VPC > Route Tables**.
2. Select the route table associated with **My VPC Public Subnet**.
3. Under the **Routes** tab, you will see:
   - A `local` route (for internal VPC traffic)
   - A route to the Internet via **Internet Gateway**
4. Click **Edit routes**.
5. Add a new route:
   - **Destination**: `10.10.0.0/16` (CIDR block of HG VPC)
   - **Target**: Select the **Peering Connection**

### Update HG VPC Route Table

Repeat similar steps for **HG VPC**:

1. Go to **Route Tables**.
2. Select the route table associated with **HG VPC Public Subnet**.
3. Click **Edit routes**.
4. Add a route:
   - **Destination**: `172.31.0.0/16` (CIDR block of My VPC)
   - **Target**: Select the **Peering Connection**

### Ping Test Between Private IPs

- Reconnect to EC2 instance in My VPC using its **public IP**.
- Attempt to ping the **private IP** of EC2 in HG VPC:
  ```bash
  ping <private-ip-of-HG-EC2>
