---
title : "Seed dữ liệu ứng dụng"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.7.1. </b> "
---

#### Mục tiêu

Seed demo users và dữ liệu bệnh viện sau khi Cognito và DynamoDB đã tồn tại.

#### Cách A - AWS Console

1. Mở **DynamoDB** và thêm sample records thủ công nếu cần.
2. Mở **Cognito** và tạo demo users thủ công nếu cần.
3. Kiểm tra roles và sample data đã có.

![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/dynamodb.png)
![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/cognito.png)
![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/cognito_1.png)

#### Cách B - Lệnh / code deployment

```powershell
$DatasetRoot = "D:\AWS\Project\Hospital_Dataset_Reset_V2_1"
$ProjectRoot = "D:\AWS\LabRuns\MedChainAI-CommandRun\Project_Hospital_AWS_P2TB"
cd $DatasetRoot
.\RESET_AND_SEED_DATASET.ps1 `
  -ProjectRoot $ProjectRoot `
  -Profile $Profile `
  -Region $Region `
  -StackName $StackName `
  -Mode Full `
  -Confirmation "RESET-HOSPITAL-DATA"
```

#### Kiểm tra

DynamoDB cần có demo patients, doctors, appointments và invoices.
