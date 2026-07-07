---
title : "Tạo CDK bootstrap resources"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.4.3. </b> "
---


#### Mục tiêu

Tạo CDK bootstrap stack và artifact bucket trước khi deploy application stack.

#### Cách A - AWS Console

1. Mở **CloudFormation**.
2. Kiểm tra `CDKToolkit` đã tồn tại chưa.
3. Mở **S3** và kiểm tra CDK asset bucket sau khi bootstrap.

![CDKToolkit console](/images/5-Workshop/5.4-AWS-Foundation/5.4.3-cdk-bootstrap/cdk.png)

#### Cách B - Lệnh / code deployment

```powershell
$AccountId = aws sts get-caller-identity --profile $Profile --query Account --output text
npm install
npm --prefix web install
npx cdk bootstrap aws://$AccountId/$Region --profile $Profile
```

#### Kiểm tra

```powershell
aws cloudformation describe-stacks `
  --stack-name CDKToolkit `
  --region $Region `
  --profile $Profile `
  --query "Stacks[0].StackStatus" `
  --output text
```
![CDKToolkit console](/images/5-Workshop/5.4-AWS-Foundation/5.4.3-cdk-bootstrap/cdk_1.png)