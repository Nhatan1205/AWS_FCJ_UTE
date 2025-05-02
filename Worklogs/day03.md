# Practise module 1 on labs

## 1. Lab 000001
Link lab01: `https://000001.awsstudygroup.com/vi/`
### Part 1: Create an AWS account
+ **MFA (Multi-factor Authentication)**: MFA is an advanced security feature for AWS accounts. When enabled, you will need to enter an OTP (One-time Password) code each time you log in to your AWS account, creating a second layer of protection in addition to the regular password.
+ **IAM Group**: IAM Group is an AWS user management tool that allows multiple IAM Users to be grouped into a group. All IAM Users in the same group will inherit the permissions assigned to that group, making permission management easier.
+ **IAM User**: IAM User is a user unit in AWS. Each IAM User has its own login information and is granted specific access to AWS resources. IAM User is created to grant long-term access to AWS accounts.
+ **AWS Support**: AWS Support is an AWS customer support service provider that helps resolve technical issues and assist with account authentication.
+ **AWS Management Console**: AWS Management Console is a web interface that allows you to manage and interact with AWS services in an intuitive way.

![image](https://github.com/user-attachments/assets/47c12f04-6b4e-4e56-9e3f-e3251b26ce0d)

### Part 2: Set up virtual MFA Device
![image](https://github.com/user-attachments/assets/e56bda76-3477-49b9-a86d-4037862acb48)

### Part 3: Create admin group and admin user
#### 3.1: Create admin group
+ Step 1: Log in to the AWS Management Console at https://aws.amazon.com/
+ Step 2: Click on your account name in the upper right corner and select `My Security Credentials`
+ Step 3: In the left navigation pane, select `User Groups` and click `Create Group`
+ Step 4: In the `User group name` field, enter the group name (e.g. AdminGroup)
+ Step 5: In the `Attach permissions policies` section, find and select the `AdministratorAccess` policy. Then select `Create Group`
+ Step 6: The group has been successfully created
![image](https://github.com/user-attachments/assets/5c7f9c54-1688-4065-ae43-640dd3d87205)

#### 3.2: Create admin user
+ Step 1: In the navigation pane, select `Users` and click `Add users`
+ Step 2: Configure user information:
  + Enter `User name` (e.g. AdminUser)
  + Select `AWS Management Console access`
  + Select `Programmatic access`
  + Select `Custom password` and enter password
  + Uncheck `User must create a new password at next sign-in`
  + Click `Next: Permissions`

![image](https://github.com/user-attachments/assets/dc136203-5f04-4908-86cb-b9b98d91d0aa)

+ Step 3: Select the `Add user to group` tab and select the created `AdminGroup` group
+ Step 4: Click `Next: Tags` (Tags are optional for organizing and managing resources)
+ Step 5: Click `Next: Review`
+ Step 6: Recheck the information and select `Create user`
+ Step 7: Download the .csv file containing the access key (if required)
+ Step 8: User has been successfully created

![image](https://github.com/user-attachments/assets/a0c6e456-fe66-47bd-a605-165f400fb9cd)

#### 3.3: Sign in with Admin user
+ Step 1: In the IAM console, select `Users` in the navigation pane
+ Step 2: Select the IAM user you just created
+ Step 3: In the `Security credentials` tab, copy the console sign-in link

![image](https://github.com/user-attachments/assets/884fe420-b30b-4a4e-a436-7be03042e6a7)

+ Step 4: Open a new incognito tab and access the sign-in link
+ Step 5: Enter the login information:
  + IAM user name
  + Created password
  + Click `Sign in`
+ Step 6: Login successful with IAM user

![image](https://github.com/user-attachments/assets/b1b234c8-41c7-4286-93e4-04f35985dcfb)

In admin user, we also can `assign MFA`, `Update console passowrd`, `create access key`. Link: https://000001.awsstudygroup.com/vi/3-create-admin-user-and-group/

![image](https://github.com/user-attachments/assets/754c1da2-e08d-4b83-aaae-a17e9ae52bdd)

### Part 4: Account authentication support
+ Step 1: Go to AWS Support console, select `Create case`. Link: https://support.console.aws.amazon.com/support/home#
  
![image](https://github.com/user-attachments/assets/cee225ce-fda1-4447-909e-d20796fc050c)

+ Step 2: Select `Account and billing support` and enter the support information:
  + Type: select `Account`.
  + Category: select `Activation`.
  + Subject: briefly describe the situation you are experiencing (eg: `Did not receive an SMS message or call for verification`)
  + Description: Provide details of the situation and information about the time you need support to activate your account.
  + Attachments: Attach an image describing the authentication step you are experiencing.
+ Step 3: In `Contact options`, select `Chat` under `Contact methods`.
+ Step 4: Select `Submit`.
+ Step 5: AWS Support team will contact and assist in activating your account..
