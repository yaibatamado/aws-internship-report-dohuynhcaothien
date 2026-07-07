---
title : "Tạo và kiểm tra data, auth, API resources"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.6.2. </b> "
---

#### Mục tiêu

Kiểm tra stack đã tạo DynamoDB, S3, Cognito, Lambda và API Gateway.

#### Cách A - AWS Console

1. Mở **DynamoDB** và kiểm tra table.
2. Mở **S3** và kiểm tra buckets.
3. Mở **Cognito** và kiểm tra user pool/groups.
4. Mở **Lambda** và **API Gateway** để kiểm tra APIs.

![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/dynamodb.png)
![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/s3.png)
![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/cognito.png)
![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/cognito_1.png)
![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/lambda.png)

#### Cách B - Lệnh / code deployment

```powershell
aws cloudformation describe-stacks `
  --stack-name $StackName `
  --region $Region `
  --profile $Profile `
  --query "Stacks[0].Outputs[*].[OutputKey,OutputValue]" `
  --output table
```

#### Kiểm tra

Outputs cần có API endpoint, CloudFront domain, bucket names, table name và user pool ID.

![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/code.png)
