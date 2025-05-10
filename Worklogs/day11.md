# **Day 11: Practice with VPC (2)**

## **Lab 03-04.1 - Create EC2 Instances in Subnets**

### **Steps to Create EC2 Instances:**

1. **Access EC2 Service:**
   - Go to the **EC2 Dashboard** from your AWS Management Console.

2. **Launch Instance:**
   - Click **Launch Instance** to start the creation process.
   - **Select an AMI (Amazon Machine Image)**: Choose the second free-tier eligible AMI (Amazon Linux 2 or Ubuntu recommended for the free tier).

3. **Choose Instance Type:**
   - Select the **t2.micro** instance type (eligible for the free tier).

4. **Create Key Pair:**
   - Under **Key Pair**, click **Create a new key pair**.
   - Name it `public-key-pair`.
   - For security reasons, it’s recommended to use **one key pair per subnet** to manage access control.

5. **Configure Network Settings:**
   - In the **Network** section, ensure you select the VPC and subnet you previously created in Lab 03-03.
   - If you’re creating a **Public EC2 instance**, ensure that the **Auto-assign Public IP** option is enabled.
   - **Security Groups**: Assign the appropriate security group to allow inbound connections (SSH - port 22).

6. **Storage Settings:**
   - The default settings (8GB SSD) should be sufficient for testing, but you can increase the size as needed.

7. **Review and Launch:**
   - Review your instance settings and click **Launch** to start your EC2 instance.

---

## **Lab 03-04.2 - Test Connection**

To test the connection to your EC2 instance using MobaXterm or another SSH client:

1. **Install MobaXterm:**
   - Download and install **MobaXterm** on your local machine.

2. **Open MobaXterm** and start a new SSH session:
   - Select **Session** in the toolbar, then choose **SSH**.

3. **Configure SSH Session:**
   - **Remote Host**: Paste the **Public IP** address of your EC2 instance.
   - **Specify Username**: Enter `ec2-user` (or `ubuntu` if using Ubuntu).
   - **Port**: Set the port to **22**.
   - **Private Key**: Under **Advanced SSH Settings**, choose the private key (`.pem` file) you created earlier during the EC2 instance setup.

4. **Test SSH Connection:**
   - Once connected, try pinging a public domain to verify internet connectivity:  
     `ping amazon.com -c 5`

5. **Ping EC2-Private Instance:**
   - Next, try pinging the **Private EC2 instance** by its **Private IP** address:  
     `ping 10.10.3.45` (replace with your actual private IP).

---

## **Lab 03-04.3 - Create NAT Gateway**

A **NAT Gateway** allows instances in private subnets to access the internet, while remaining inaccessible from the public internet.

1. **Allocate Elastic IP Address:**
   - Go to **VPC** in the AWS Console.
   - In the **Elastic IPs** section, click **Allocate Elastic IP address**.
   - Add a tag with the name **Name** (e.g., `NAT-Gateway-IP`), and click **Allocate**.

2. **Create NAT Gateway:**
   - Go to **NAT Gateways** in the VPC Dashboard and click **Create NAT Gateway**.
   - Provide a **name** for the NAT Gateway (e.g., `route-private`).
   - **Subnet**: Select the **public subnet** where the NAT Gateway will reside.
   - **Elastic IP**: Select the Elastic IP you just created.

3. **Configure Route Table for NAT Gateway:**
   - After creating the NAT Gateway, go to the **Route Tables** section in the VPC Dashboard.
   - Select the **Private Route Table** associated with the private subnet(s).
   - Click **Edit Route Table** to add a new route:
     - **Destination**: `0.0.0.0/0` (all internet traffic).
     - **Target**: Select the newly created **NAT Gateway**.

4. **Edit Subnet Associations:**
   - In the Route Table, click on **Subnet Associations** and click **Edit**.
   - Select the **Private Subnets** that need internet access via the NAT Gateway.
   - Click **Save**.

---

## **Lab 03-04.4 - Verify NAT Gateway Connectivity**

1. **Launch a New EC2 Instance in a Private Subnet:**
   - Launch a new EC2 instance in your **Private Subnet**.
   - **Public IP**: Do not assign a public IP since it will access the internet through the NAT Gateway.

2. **Test Internet Access:**
   - SSH into the private EC2 instance (using the public EC2 instance as a jump host, if necessary).
   - Test internet connectivity by running:  
     `ping google.com -c 5`

   If the private instance can successfully ping external addresses, the **NAT Gateway** configuration is correct.

---

## **Conclusion**
In this lab, you've learned how to:
- Create **EC2 instances** in both public and private subnets.
- **Test SSH connectivity** to EC2 instances.
- Set up a **NAT Gateway** to allow internet access for instances in private subnets.
- Modify **Route Tables** to ensure proper traffic flow through the NAT Gateway.

This lab provides the foundational knowledge required for managing VPCs, creating instances, and configuring network access in a secure and efficient manner.

---

