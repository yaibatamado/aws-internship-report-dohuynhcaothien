---
title : "Configure VNPay IPN and Return URL"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.8.1. </b> "
---

#### Goal

Configure VNPay callback URLs after the CloudFront domain is available.

#### Method A - VNPay Sandbox portal

1. Open VNPay Sandbox configuration.
2. Set Return URL to `https://<cloudfront-domain>/api/payment/vnpay-return`.
3. Set IPN URL to `https://<cloudfront-domain>/api/payment/vnpay-ipn`.
4. Do not add `#` before the URL.

![VNPay IPN](/images/5-Workshop/5.8-Integration-Test/5.8.1-vnpay-url/vnpay.png)

#### Method B - Command / code deployment

```powershell
$CloudFrontDomain = aws cloudformation describe-stacks `
  --stack-name $StackName `
  --region $Region `
  --profile $Profile `
  --query "Stacks[0].Outputs[?contains(OutputKey,'CloudFront')].OutputValue | [0]" `
  --output text

$AppBaseUrl = "https://$CloudFrontDomain"
$env:VNPAY_RETURN_URL = "$AppBaseUrl/api/payment/vnpay-return"
$env:VNPAY_IPN_URL = "$AppBaseUrl/api/payment/vnpay-ipn"

"Return: $env:VNPAY_RETURN_URL"
"IPN: $env:VNPAY_IPN_URL"
```

#### Validation

Create a test payment and verify that the VNPay Sandbox payment page opens.
