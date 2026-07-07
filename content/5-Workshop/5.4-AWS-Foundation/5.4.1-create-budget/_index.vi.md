---
title : "Tạo budget và chọn region"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.4.1. </b> "
---


#### Mục tiêu

Tạo budget alert và xác nhận region trước khi tạo bất kỳ tài nguyên nào.

#### Cách A - AWS Console

1. Mở **Billing and Cost Management**.
2. Chọn **Budgets**.
3. Tạo monthly cost budget cho lab.
4. Thêm email notification.
5. Chọn **ap-southeast-1** trong AWS region selector cho tài nguyên ứng dụng.

![Budget result](/images/5-Workshop/5.4-AWS-Foundation/5.4.1-create-budget/create-budgets-1.png)
![Budget result](/images/5-Workshop/5.4-AWS-Foundation/5.4.1-create-budget/create-budgets-2.png)
![Budget result](/images/5-Workshop/5.4-AWS-Foundation/5.4.1-create-budget/create-budgets-3.png)

#### Cách B - Lệnh / code deployment

```powershell
$Profile = "hospital-dev"
$Region = "ap-southeast-1"
$AccountId = aws sts get-caller-identity --profile $Profile --query Account --output text

aws budgets create-budget `
  --account-id $AccountId `
  --budget '{"BudgetName":"MedChainAI-Lab-Budget","BudgetLimit":{"Amount":"10","Unit":"USD"},"TimeUnit":"MONTHLY","BudgetType":"COST"}' `
  --profile $Profile
```

