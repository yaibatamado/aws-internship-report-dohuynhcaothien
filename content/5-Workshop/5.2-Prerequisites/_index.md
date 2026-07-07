---
title : "Prerequisites"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

#### Prerequisites

Before starting the lab, prepare the following items:

+ AWS account with billing access.
+ AWS CLI configured on the local machine.
+ Node.js and npm.
+ AWS CDK CLI.
+ Git and PowerShell.
+ VNPay Sandbox merchant information.
+ Permission to create Amazon Managed Blockchain Ethereum node.

The website and backend callbacks will use the CloudFront distribution domain.

#### Local tool check

```powershell
node --version
npm --version
aws --version
git --version
```

![Local tools](/images/5-Workshop/5.2-Prerequisites/local.png)

#### IAM permission note

Attach a deploy policy to the IAM user or role that runs the lab. For a student lab, the deployer needs permissions for CloudFormation, S3, DynamoDB, Lambda, API Gateway, Cognito, CloudFront, Secrets Manager, CloudWatch, Managed Blockchain, and IAM PassRole.

#### Create a new lab workspace

Do not run command-based deployment directly inside the main project folder. Create a separate folder for screenshots and command evidence.

```powershell
$LabRoot = "D:\AWS\LabRuns\MedChainAI-CommandRun"
New-Item -ItemType Directory -Path $LabRoot -Force | Out-Null
cd $LabRoot
```
![Region và budget AWS](/images/5-Workshop/5.2-Prerequisites/aws_region.png)
![Region và budget AWS](/images/5-Workshop/5.2-Prerequisites/iam.png)
![Region và budget AWS](/images/5-Workshop/5.2-Prerequisites/pttt.png)
