# Day 16: Practice with CloudFormation Template, CloudFront, and RDGW (Remote Desktop Gateway)

## Lab10-02.2 – Initialize a CloudFormation Template

### 📝 Overview

**AWS CloudFormation** is a service that allows you to model and manage AWS infrastructure using **Infrastructure as Code (IaC)**. Instead of manually creating resources such as EC2, S3, RDS, or VPC through the AWS Console, you can define them in a **YAML** or **JSON** template file. CloudFormation will then automatically provision these resources in the correct order and with your defined configuration.

---

### 🚀 Steps to Deploy Resources Using a CloudFormation Template

#### Step 1: Access CloudFormation

- Open the **CloudFormation** service from the AWS Management Console.
- Click **“Create Stack”**.
- Choose **“With new resources (standard)”**.

#### Step 2: Specify the Template

Choose one of the following:
- **Amazon S3 URL**: Enter the URL of the CloudFormation template stored in an S3 bucket.
- **Upload a Template File**: Upload a `.yaml` or `.json` file from your local system.
- *(Optional)* You may also choose the **Designer** tool for a visual drag-and-drop experience.

#### Example CloudFormation Template (EC2, YAML)

```yaml
Resources:
  MyEC2Instance:
    Type: "AWS::EC2::Instance"
    Properties:
      InstanceType: t3.micro
      ImageId: ami-0abcdef1234567890
      KeyName: my-keypair
      NetworkInterfaces:
        - AssociatePublicIpAddress: true
          DeviceIndex: 0
          SubnetId: subnet-xxxxxx
          GroupSet:
            - sg-xxxxxx
```

#### Step 3: Stack Configuration
- Click **Next** after uploading or linking your template.

#### Step 4: Stack Details
- **Stack name**: Provide a name for the stack.
- **Availability Zones (AZs)**: Choose at least **2** for high availability.
- **VPC Settings**:
  - **VPC Tenancy**: Keep **default**.
  - **VPC CIDR**: `10.0.0.0/16`
  - Leave **public/private CIDR ranges** as default.
- **Remote Access**:
  - **Allow RDP from anywhere**: `0.0.0.0/0` on port **3389**
- **Key Pair**: Select an **existing key pair**
- **Instance Type**: Use small instance types like `t3.micro`
- **Admin Password**: Choose a password that includes both **letters and numbers**
- **Application Insights**: Set to **false**

#### Step 5: Stack Options
- Click **Next** to go through advanced options.
- Leave them as **default** if not needed.

#### Step 6: Review and Create
- Review all settings.
- Tick **both checkboxes** for acknowledging IAM resource creation.
- Click **Create Stack**.

---

## 🔍 Monitoring Resource Creation
- In the **stack page**, go to the **Events** tab to see provisioning progress.
- Go to the **Outputs** tab for details like **instance public IP**, etc.
- Check the **Resources** tab to confirm creation of:
  - EC2
  - EIP
  - Load Balancer
  - Auto Scaling Group
  - VPC
  - Other resources
- Use the **Template** tab to inspect the source YAML/JSON used.

---

## Lab10-02.3 – Configure Security Group

### 🔐 Configure Inbound Rule for RDP Access
1. Go to **EC2 Dashboard** → **Security Groups** (under *Network & Security*).
2. Find the **security group** associated with your EC2 instance.
3. Click **Edit Inbound Rules**.
4. Add a rule with the following settings:
   - **Type**: RDP
   - **Protocol**: TCP
   - **Port Range**: `3389`
   - **Source**: `0.0.0.0/0` (⚠️ Allows access from any IP – use with caution)

---

## Lab10-03 – Connect to RDGW (Remote Desktop Gateway)

### 🖥️ Connect to Your EC2 Instance via Remote Desktop
1. In the **EC2 Dashboard**, select the **running instance**.
2. Click the **Connect** button at the top.
3. Select the **RDP Client** tab.
4. Click **Download Remote Desktop File** to download the `.rdp` file.
5. Click **Get Password**:
   - Upload your **.pem private key file** (used when launching the instance).
   - Click **Decrypt Password** to retrieve the admin password.
6. Open the `.rdp` file and choose **Connect**.
7. Enter the **decrypted password** when prompted.

