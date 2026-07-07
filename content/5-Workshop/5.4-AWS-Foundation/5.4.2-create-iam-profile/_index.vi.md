---
title : "Tạo IAM deployer và local profile"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.4.2. </b> "
---


#### Mục tiêu

Tạo deploy identity và kiểm tra command line có thể truy cập AWS.

#### Cách A - AWS Console

1. Mở **IAM**.
2. Tạo user hoặc role tên `medchain-ai-lab-deployer`.
3. Gắn lab deploy policy.
4. Tạo access key nếu dùng AWS CLI.
5. Không chụp secret access key.

![IAM deployer](/images/5-Workshop/5.4-AWS-Foundation/5.4.2-create-iam-profile/iam_1.png)
![IAM deployer](/images/5-Workshop/5.4-AWS-Foundation/5.4.2-create-iam-profile/iam_2.png)
![IAM deployer](/images/5-Workshop/5.4-AWS-Foundation/5.4.2-create-iam-profile/iam_3.png)
![IAM deployer](/images/5-Workshop/5.4-AWS-Foundation/5.4.2-create-iam-profile/iam_4.png)
![IAM deployer](/images/5-Workshop/5.4-AWS-Foundation/5.4.2-create-iam-profile/iam_5.png)

#### Cách B - Lệnh / code deployment

```powershell
aws configure --profile hospital-dev
aws sts get-caller-identity --profile hospital-dev
```

![IAM deployer](/images/5-Workshop/5.4-AWS-Foundation/5.4.2-create-iam-profile/iam_6.png)

#### Kiểm tra

Command phải trả về `Account`, `UserId` và `Arn`.
