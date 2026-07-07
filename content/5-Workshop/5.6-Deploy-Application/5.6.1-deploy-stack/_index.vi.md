---
title : "Tạo application stack"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.6.1. </b> "
---

#### Mục tiêu

Deploy main MedChain AI stack sau khi pre-stack services đã sẵn sàng.

#### Cách A - AWS Console

1. Mở **CloudFormation**.
2. Create stack từ synthesized template nếu deploy thủ công.
3. Nhập stack name `MedChainAiLabStack`.
4. Chờ **CREATE_COMPLETE**.

![Stack complete](/images/5-Workshop/5.6-Deploy-Application/5.6.1-deploy-stack/stack.png)

#### Cách B - Lệnh / code deployment

```powershell
$env:ENABLE_API_ROUTES = "true"
$env:ENABLE_WEEK3_OPERATIONS = "true"
$env:RETAIN_DATA = "false"
$env:ENABLE_CLOUDFRONT = "true"
$env:USE_EXISTING_CLOUDFRONT = "false"
npx cdk synth $StackName --profile $Profile
npx cdk deploy $StackName --profile $Profile --require-approval never
```

#### Kiểm tra

CloudFormation stack phải CREATE_COMPLETE và có outputs.

![Stack complete](/images/5-Workshop/5.6-Deploy-Application/5.6.1-deploy-stack/stack_1.png)
