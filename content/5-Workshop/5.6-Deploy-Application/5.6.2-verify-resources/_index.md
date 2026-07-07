---
title : "Create and verify data, auth, API resources"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.6.2. </b> "
---

#### Goal

Confirm that the stack created DynamoDB, S3, Cognito, Lambda and API Gateway resources.

#### Method A - AWS Console

1. Open **DynamoDB** and verify the table.
2. Open **S3** and verify buckets.
3. Open **Cognito** and verify user pool/groups.
4. Open **Lambda** and **API Gateway** and verify APIs.

![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/dynamodb.png)
![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/s3.png)
![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/cognito.png)
![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/cognito_1.png)
![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/lambda.png)

#### Method B - Command / code deployment

```powershell
aws cloudformation describe-stacks `
  --stack-name $StackName `
  --region $Region `
  --profile $Profile `
  --query "Stacks[0].Outputs[*].[OutputKey,OutputValue]" `
  --output table
```

#### Validation

Outputs should include API endpoint, CloudFront domain, bucket names, table name and user pool ID.
![Stack outputs](/images/5-Workshop/5.6-Deploy-Application/5.6.2-verify-resources/code.png)
