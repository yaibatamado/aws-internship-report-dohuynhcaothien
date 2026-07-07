---
title : "Build and upload web frontend"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.7.2. </b> "
---

#### Goal

Build the frontend and upload generated files to the frontend S3 bucket.

#### Method A - AWS Console

1. Build frontend locally.
2. Open **S3** and select frontend bucket.
3. Upload files from `web/dist`.
4. Confirm `index.html` and `assets/` exist.

![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/create-s3-5.png)
![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/cloudfront-created.png)
![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/cloudfront-web.png)

#### Method B - Command / code deployment

```powershell
cd "D:\AWS\LabRuns\MedChainAI-CommandRun\Project_Hospital_AWS_P2TB"
npm --prefix web run build
$FrontendBucket = aws cloudformation describe-stacks --stack-name $StackName --region $Region --profile $Profile --query "Stacks[0].Outputs[?contains(OutputKey,'FrontendBucket')].OutputValue | [0]" --output text
aws s3 sync .\web\dist "s3://$FrontendBucket" --profile $Profile
```

#### Validation

S3 frontend bucket should contain `index.html` and built assets.
