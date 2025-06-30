# Practise module 1 on lab
## 1. Lab 000007
Link lab07 : https://000007.awsstudygroup.com/vi/

AWS Budget is a service that provides the ability to set up budgets that alert you when costs exceed (or are forecast to exceed) your budget.

AWS Budget includes four budget types:
+ Cost Budget
+ Usage Budget
+ RI Budget
+ Savings Plans Budget

### Benefits of Using AWS Budget

Using AWS Budget brings many benefits to businesses:
+ Cost Control: Helps you proactively monitor and control AWS costs.
+ Timely Alerts: Get notified as soon as costs exceed set thresholds.
+ Financial Planning: Supports financial planning and forecasting of future costs.
+ Resource Optimization: Identify high-cost services to optimize usage.
+ Cost Allocation: Easily allocate costs to different projects, departments, or customers.
### Steps to Set Up an Effective AWS Budget
+ Define Budget Goals: Understand your needs and spending limits.
+ Analyze Current Costs: Review current costs to set a reasonable budget.
+ Set Alert Thresholds: Set alert thresholds at appropriate levels (usually 80% and 100% of budget).
+ Configure notifications: Ensure notifications are sent to the right people.
+ Monitor and adjust: Regularly review and adjust budgets as needed.
### Part 1: Create Budget by Template
+ Step 1: Access the **AWS Management Console** and navigate to **AWS Billing and Cost Management**:
    + Sign in to the AWS Console
    + Search for and select **Billing and Cost Management** in the services search bar

+ Step 2: Navigate to the Budgets section:
    + In the left navigation pane, select **Budgets**
    + Click the **Create a budget** button
  ![image](https://github.com/user-attachments/assets/87e12d13-7e6b-4dce-a556-3eaaa5dbb6c6)

+ Step 3: Select the template option for budget setup:
    + Choose **Use a template (simplified)**
    + From the available templates, select **Monthly cost budget**
  ![image](https://github.com/user-attachments/assets/da03f19f-348d-438e-b43c-b203aeeb3bb4)

+ Step 4: Configure your budget settings:
    + Enter a descriptive name for your budget
    + Set your monthly budget amount
    + Review the email recipients for alerts
    + Click **Create budget** to finalize
  ![image](https://github.com/user-attachments/assets/0093547a-7f22-4def-be70-a53ff6b60695)

+ Step 5: Verify your budget has been created successfully:
    + You should see a confirmation message
    + Your new budget will appear in the budgets list
  ![image](https://github.com/user-attachments/assets/49d27d06-8675-4608-be0e-9be270101133)

+ Step 6: View your budget history:
    + Select your newly created budget
    + Navigate to the **Budget history** tab to see historical performance

+ Step 7: Review the budget overview:
    + The overview provides a snapshot of your current spending against your budget
    + Visual indicators show your budget status at a glance

+ Step 8: Monitor budget health and alerts:
    + Check the **Budget health** section to see your current status
    + Review any active alerts that have been triggered

+ Step 9: Return to the budget history for trend analysis:
    + Historical data helps identify spending patterns over time
    + Use this information to refine future budgets

+ Step 10: Understand the template alert configuration:
    + Review the alert thresholds and notification settings
    + Note how the template has configured both actual and forecasted alerts

### Part 2: Creating a Cost Budget
+ Step 1: Sign in to the **AWS Management Console** and search for **AWS Billing and Cost Management** in the services search bar.
  
+ Step 2: In the navigation pane, select **Budgets**.
  
+ Step 3: Click **Create budget**.
  
+ Step 4: Configure your **Budget setup**:
    + Select **Customize (advanced)** for more control over your budget settings
    + Under **Budget types**, select **Cost budget**
    + Click **Next**
    
+ Step 5: In the **Set your budget** section:
    + Enter a descriptive **Budget name** (e.g., Monthly)
    + For **Period**, select the appropriate time interval:
        + **Daily** for day-to-day monitoring
        + **Monthly** for month-to-month tracking (most common)
        + **Quarterly** for quarterly oversight
        + **Annually** for yearly budget management
    + Under **Budget effective dates**:
        + Select **Recurring Budget** if you want this budget to continue indefinitely
        + Select **Expiring Budget** if you need a one-time budget for a specific timeframe
        + Note that all time zones are in **UTC**
    + In the **Specify your monthly budget** section:
        + Choose **Fixed** to set the same budget amount for each period
        + Choose **Monthly Budget Planning** to set different amounts for each period
        + Enter your **Budgeted amount** in your preferred currency
    ![image](https://github.com/user-attachments/assets/fb37c846-cb91-4dbe-98d6-cb0c7f0f9c62)

+ Step 6: For **Budget scope**, select **All AWS services** to monitor your entire AWS spending, then click **Next**.
    ![image](https://github.com/user-attachments/assets/79670365-18c5-4487-bb82-0f7bde120173)

+ Step 7: In the **Configure alerts** section, click **Add an alert threshold**, then click **Next**.
  
+ Step 8: Configure your alert settings:
    + Set the threshold percentage (e.g., 80% of actual or forecasted spend)
    + Add email recipients who should receive notifications
    + Optionally, configure an Amazon SNS topic for programmatic notifications
    + Click Next 
  ![image](https://github.com/user-attachments/assets/bf8c7115-e944-482d-b931-5926bccf7ea0)

+ Step 9: Review the budget actions settings and click **Next**.
  
+ Step 10: Review your budget configuration and click **Create budget**.
  
+ Step 11: Verify that your budget has been created successfully.

### Part 3: Create Usage Budget
+ Step 1: Sign in to the **AWS Management Console** and search for **AWS Billing and Cost Management** in the services search bar.
+ Step 2: In the navigation pane, select **Budgets**.
+ Step 3: Click **Create budget**.
+ Step 4: Configure your **Budget setup**:
    + Select **Customize (advanced)** for more control over your budget settings
    + Under **Budget types**, select **Usage budget**
    + Click **Next**
+ Step 5: In the **Details** section, enter a descriptive name for your budget.
+ Step 6: For **Usage type**, select **Use type groups**:
    + Choose **EC2:Running Hours** from the dropdown menu
+ Step 7:
+ Step 8:
+ Step 9:
+ Step 10:
+ Step 11:
+ Step 12:
+ Step 13:
+ Step 14:
+ Step 15:
