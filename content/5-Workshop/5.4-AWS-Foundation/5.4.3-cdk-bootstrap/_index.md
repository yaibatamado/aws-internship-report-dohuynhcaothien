---
title : "Create CDK bootstrap resources"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.4.3. </b> "
---


#### Goal

Create the CDK bootstrap stack and artifact bucket before deploying the application stack.

#### Method A - AWS Console

1. Open **CloudFormation**.
2. Check whether `CDKToolkit` exists.
3. Open **S3** and check the CDK asset bucket after bootstrap.

![CDKToolkit console](/aws-internship-report-dohuynhcaothien/images/5-Workshop/5.4-AWS-Foundation/5.4.3-cdk-bootstrap/cdk.png)

#### Method B - Command / code deployment

```powershell
$AccountId = aws sts get-caller-identity --profile $Profile --query Account --output text
npm install
npm --prefix web install
npx cdk bootstrap aws://$AccountId/$Region --profile $Profile
```

![CDK bootstrap command](/aws-internship-report-dohuynhcaothien/images/5-Workshop/5.4-AWS-Foundation/5.4.3-cdk-bootstrap/cdk_1.png)

#### Validation

```powershell
aws cloudformation describe-stacks `
  --stack-name CDKToolkit `
  --region $Region `
  --profile $Profile `
  --query "Stacks[0].StackStatus" `
  --output text
```
