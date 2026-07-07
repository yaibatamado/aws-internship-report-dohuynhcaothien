---
title : "Chuẩn bị VNPay Sandbox"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.5.1. </b> "
---

#### Mục tiêu

Chuẩn bị thông tin VNPay Sandbox trước khi deploy payment backend.

#### Cách A - VNPay Sandbox portal

1. Đăng ký hoặc yêu cầu tài khoản merchant VNPay Sandbox.
2. Lấy **TMN Code**.
3. Lấy **Hash Secret** và lưu an toàn.
4. Chưa cấu hình IPN/Return URL ở bước này. Các URL này chỉ có sau khi CloudFront được tạo.

![Thông tin VNPay](/images/5-Workshop/5.5-Pre-Stack-Services/5.5.1-vnpay/vnpay.png)

#### Cách B - Biến môi trường

```powershell
$env:VNPAY_PAYMENT_URL = "https://sandbox.vnpayment.vn/paymentv2/vpcpay.html"
$env:VNPAY_TMN_CODE = "YOUR_TMN_CODE"
$env:VNPAY_HASH_SECRET = "YOUR_HASH_SECRET"
```

#### Kiểm tra

TMN Code và Hash Secret phải sẵn sàng trước khi deploy application stack.
