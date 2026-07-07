---
title : "Invalidate CloudFront and open website"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.7.3. </b> "
---

#### Goal

Refresh CloudFront cache and open the deployed website.

#### Method A - AWS Console

1. Open **CloudFront**.
2. Select the distribution.
3. Create invalidation for `/*`.
4. Open the distribution domain.

![CloudFront behaviors](/images/5-Workshop/5.6-Deploy-Application/5.6.3-cloudfront/cloudfront-web.png)

#### Method B - Command / code deployment

```powershell
$DistributionId = aws cloudformation describe-stacks --stack-name $StackName --region $Region --profile $Profile --query "Stacks[0].Outputs[?contains(OutputKey,'DistributionId')].OutputValue | [0]" --output text
$Invalidation = aws cloudfront create-invalidation --distribution-id $DistributionId --paths "/*" --profile $Profile | ConvertFrom-Json
aws cloudfront wait invalidation-completed --distribution-id $DistributionId --id $Invalidation.Invalidation.Id --profile $Profile
```

#### Validation

The browser should show MedChain AI homepage.
