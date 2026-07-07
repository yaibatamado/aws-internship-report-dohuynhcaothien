---
title : "Create IAM deployer and local profile"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.4.2. </b> "
---


#### Goal

Create a deploy identity and verify that the command line can access AWS.

#### Method A - AWS Console

1. Open **IAM**.
2. Create a user or role named `medchain-ai-lab-deployer`.
3. Attach the lab deploy policy.
4. Create an access key if you use AWS CLI.
5. Do not capture secret access key in screenshots.

![IAM deployer](/images/5-Workshop/5.4-AWS-Foundation/5.4.2-create-iam-profile/iam_1.png)
![IAM deployer](/images/5-Workshop/5.4-AWS-Foundation/5.4.2-create-iam-profile/iam_2.png)
![IAM deployer](/images/5-Workshop/5.4-AWS-Foundation/5.4.2-create-iam-profile/iam_3.png)
![IAM deployer](/images/5-Workshop/5.4-AWS-Foundation/5.4.2-create-iam-profile/iam_4.png)
![IAM deployer](/images/5-Workshop/5.4-AWS-Foundation/5.4.2-create-iam-profile/iam_5.png)


#### Method B - Command / code deployment

```powershell
aws configure --profile hospital-dev
aws sts get-caller-identity --profile hospital-dev
```

![IAM deployer](/images/5-Workshop/5.4-AWS-Foundation/5.4.2-create-iam-profile/iam_6.png)

#### Validation

The command must return `Account`, `UserId`, and `Arn`.
