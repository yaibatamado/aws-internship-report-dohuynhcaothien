---
title : "Tạo CloudFront distribution cho frontend"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.6.3. </b> "
---

#### Mục tiêu

Tạo hoặc kiểm tra CloudFront distribution dùng để phục vụ frontend và chuyển tiếp request backend API. CloudFront distribution domain là URL public của ứng dụng.

#### Cách A - AWS Console

1. Mở **CloudFront** và kiểm tra distribution.
2. Kiểm tra default behavior trỏ đến S3 frontend origin.
3. Kiểm tra behavior `/api/*` trỏ đến API Gateway.
4. Copy CloudFront distribution domain, ví dụ `dxxxxx.cloudfront.net`.

![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/create-s3-1.png)
![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/create-s3-2.png)
![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/create-s3-3.png)
![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/create-s3-4.png)
![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/create-s3-5.png)
![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/create-cloudfront-1.png)
![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/create-cloudfront-2.png)
![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/create-cloudfront-3.png)
![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/create-cloudfront-4.png)
![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/create-cloudfront-5.png)
![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/cloudfront-created.png)
![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/cloudfront-web.png)


#### Cách B - Lệnh / code deployment

```powershell
$DistributionDomain = aws cloudformation describe-stacks `
  --stack-name $StackName `
  --region $Region `
  --profile $Profile `
  --query "Stacks[0].Outputs[?contains(OutputKey,'CloudFront')].OutputValue | [0]" `
  --output text

$DistributionDomain
```

#### Kiểm tra

CloudFront distribution phải có behavior cho frontend và behavior `/api/*` cho API. Website URL sẽ là `https://<cloudfront-domain>`.

![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/cloudfront_code.png)