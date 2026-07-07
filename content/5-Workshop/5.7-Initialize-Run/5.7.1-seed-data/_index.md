---
title : "Seed application data"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.7.1. </b> "
---

#### Goal

Seed demo users and hospital records after Cognito and DynamoDB exist.

#### Method A - AWS Console

1. Open **DynamoDB** and add sample records manually if needed.
2. Open **Cognito** and create demo users manually if needed.
3. Confirm roles and sample data are available.

![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/dynamodb.png)
![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/cognito.png)
![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/cognito_1.png)


#### Method B - Command / code deployment

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

#### Validation

DynamoDB should contain demo patients, doctors, appointments and invoices.
