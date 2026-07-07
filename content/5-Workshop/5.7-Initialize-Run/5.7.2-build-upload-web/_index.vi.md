---
title : "Build và upload web frontend"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.7.2. </b> "
---

#### Mục tiêu

Build frontend và upload files sinh ra lên frontend S3 bucket.

#### Cách A - AWS Console

1. Build frontend trên máy local.
2. Mở **S3** và chọn frontend bucket.
3. Upload files từ `web/dist`.
4. Kiểm tra có `index.html` và `assets/`.

![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/create-s3-5.png)
![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/cloudfront-created.png)
![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/cloudfront-web.png)

#### Cách B - Lệnh / code deployment

```powershell
cd "D:\AWS\LabRuns\MedChainAI-CommandRun\Project_Hospital_AWS_P2TB"
npm --prefix web run build
$FrontendBucket = aws cloudformation describe-stacks --stack-name $StackName --region $Region --profile $Profile --query "Stacks[0].Outputs[?contains(OutputKey,'FrontendBucket')].OutputValue | [0]" --output text
aws s3 sync .\web\dist "s3://$FrontendBucket" --profile $Profile
```

#### Kiểm tra

S3 frontend bucket cần có `index.html` và assets đã build.
