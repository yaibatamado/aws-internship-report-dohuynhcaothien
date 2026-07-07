---
title : "Create budget and choose region"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.4.1. </b> "
---


#### Goal

Create a budget alert and confirm the region before any resource is created.

#### Method A - AWS Console

1. Open **Billing and Cost Management**.
2. Choose **Budgets**.
3. Create a monthly cost budget for the lab.
4. Add an email notification.
5. Choose **ap-southeast-1** in the AWS region selector for application resources.

![Budget result](/images/5-Workshop/5.4-AWS-Foundation/5.4.1-create-budget/create-budgets-1.png)
![Budget result](/images/5-Workshop/5.4-AWS-Foundation/5.4.1-create-budget/create-budgets-2.png)
![Budget result](/images/5-Workshop/5.4-AWS-Foundation/5.4.1-create-budget/create-budgets-3.png)

#### Method B - Command / code deployment

```powershell
$Profile = "hospital-dev"
$Region = "ap-southeast-1"
$AccountId = aws sts get-caller-identity --profile $Profile --query Account --output text

aws budgets create-budget `
  --account-id $AccountId `
  --budget '{"BudgetName":"MedChainAI-Lab-Budget","BudgetLimit":{"Amount":"10","Unit":"USD"},"TimeUnit":"MONTHLY","BudgetType":"COST"}' `
  --profile $Profile
```