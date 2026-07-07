---
title : "Invalidate CloudFront và mở website"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.7.3. </b> "
---

#### Mục tiêu

Refresh CloudFront cache và mở website đã deploy.

#### Cách A - AWS Console

1. Mở **CloudFront**.
2. Chọn distribution.
3. Tạo invalidation cho `/*`.
4. Mở distribution domain.

![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/cloudfront-web.png)

#### Cách B - Lệnh / code deployment

```powershell
$DistributionId = aws cloudformation describe-stacks --stack-name $StackName --region $Region --profile $Profile --query "Stacks[0].Outputs[?contains(OutputKey,'DistributionId')].OutputValue | [0]" --output text
$Invalidation = aws cloudfront create-invalidation --distribution-id $DistributionId --paths "/*" --profile $Profile | ConvertFrom-Json
aws cloudfront wait invalidation-completed --distribution-id $DistributionId --id $Invalidation.Invalidation.Id --profile $Profile
```

#### Kiểm tra

Trình duyệt cần hiển thị trang chủ MedChain AI.
