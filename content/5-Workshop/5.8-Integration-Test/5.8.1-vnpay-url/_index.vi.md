---
title : "Cấu hình VNPay IPN và Return URL"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.8.1. </b> "
---

#### Mục tiêu

Cấu hình VNPay callback URLs sau khi CloudFront domain đã sẵn sàng.

#### Cách A - VNPay Sandbox portal

1. Mở cấu hình VNPay Sandbox.
2. Đặt Return URL là `https://<cloudfront-domain>/api/payment/vnpay-return`.
3. Đặt IPN URL là `https://<cloudfront-domain>/api/payment/vnpay-ipn`.
4. Không thêm dấu `#` trước URL.

![VNPay IPN](/images/5-Workshop/5.8-Integration-Test/5.8.1-vnpay-url/vnpay.png)

#### Cách B - Lệnh / code deployment

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

#### Kiểm tra

Tạo thanh toán thử và kiểm tra trang thanh toán VNPay Sandbox mở thành công.
