---
title : "Điều kiện chuẩn bị"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

#### Điều kiện chuẩn bị

Trước khi bắt đầu bài lab, cần chuẩn bị:

+ AWS account có quyền billing.
+ AWS CLI đã cấu hình trên máy local.
+ Node.js và npm.
+ AWS CDK CLI.
+ Git và PowerShell.
+ Thông tin merchant VNPay Sandbox.
+ Quyền tạo Amazon Managed Blockchain Ethereum node.

Website và callback backend sẽ dùng CloudFront distribution domain.

#### Kiểm tra công cụ local

```powershell
node --version
npm --version
aws --version
git --version
```

![Công cụ local](/images/5-Workshop/5.2-Prerequisites/local.png)

#### Ghi chú quyền IAM

Gắn deploy policy vào IAM user hoặc role dùng để chạy lab. Với bài lab sinh viên, deployer cần quyền cho CloudFormation, S3, DynamoDB, Lambda, API Gateway, Cognito, CloudFront, Secrets Manager, CloudWatch, Managed Blockchain và IAM PassRole.

#### Tạo workspace lab mới

Không chạy phần command deployment trực tiếp trong project chính. Hãy tạo thư mục riêng để chạy lệnh, chụp hình và lưu bằng chứng.

```powershell
$LabRoot = "D:\AWS\LabRuns\MedChainAI-CommandRun"
New-Item -ItemType Directory -Path $LabRoot -Force | Out-Null
cd $LabRoot
```

![Region và budget AWS](/images/5-Workshop/5.2-Prerequisites/aws_region.png)
![Region và budget AWS](/images/5-Workshop/5.2-Prerequisites/iam.png)
![Region và budget AWS](/images/5-Workshop/5.2-Prerequisites/pttt.png)
