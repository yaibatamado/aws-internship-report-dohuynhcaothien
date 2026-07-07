---
title : "Prepare VNPay Sandbox"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.5.1. </b> "
---

#### Goal

Prepare VNPay Sandbox information before deploying the payment backend.

#### Method A - VNPay Sandbox portal

1. Register or request a VNPay Sandbox merchant account.
2. Collect **TMN Code**.
3. Collect **Hash Secret** and store it securely.
4. Do not configure IPN/Return URL yet. These URLs will be available only after CloudFront is created.

![VNPay info](/images/5-Workshop/5.5-Pre-Stack-Services/5.5.1-vnpay/vnpay.png)

#### Method B - Environment variables

```powershell
$env:VNPAY_PAYMENT_URL = "https://sandbox.vnpayment.vn/paymentv2/vpcpay.html"
$env:VNPAY_TMN_CODE = "YOUR_TMN_CODE"
$env:VNPAY_HASH_SECRET = "YOUR_HASH_SECRET"
```

#### Validation

The TMN Code and Hash Secret must be available before the application stack is deployed.
