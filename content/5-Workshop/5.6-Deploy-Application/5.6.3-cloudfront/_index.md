---
title : "Create frontend CloudFront distribution"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.6.3. </b> "
---

#### Goal

Create or verify the CloudFront distribution that serves the frontend and forwards backend API requests. The CloudFront distribution domain is the public URL of the application.

#### Method A - AWS Console

1. Open **CloudFront** and inspect the distribution.
2. Verify the default behavior points to the S3 frontend origin.
3. Verify the `/api/*` behavior points to API Gateway.
4. Copy the CloudFront distribution domain, for example `dxxxxx.cloudfront.net`.

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


#### Method B - Command / code deployment

```powershell
$DistributionDomain = aws cloudformation describe-stacks `
  --stack-name $StackName `
  --region $Region `
  --profile $Profile `
  --query "Stacks[0].Outputs[?contains(OutputKey,'CloudFront')].OutputValue | [0]" `
  --output text

$DistributionDomain
```

#### Validation

The CloudFront distribution must show the frontend behavior and the `/api/*` API behavior. The website URL will be `https://<cloudfront-domain>`.

![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/cloudfront_code.png)