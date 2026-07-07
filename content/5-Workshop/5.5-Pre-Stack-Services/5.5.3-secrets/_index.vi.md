---
title : "Tạo Secrets Manager configuration"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.5.3. </b> "
---

#### Mục tiêu

Lưu cấu hình tích hợp trước khi application stack đọc các giá trị này.

#### Cách A - AWS Console

1. Mở **Secrets Manager**.
2. Store a new secret.
3. Thêm key-value cho VNPay và AMB.
4. Đặt tên `medchain-ai/lab/integrations`.

![Secrets created](/images/5-Workshop/5.5-Pre-Stack-Services/5.5.3-secrets/secrets.png)

#### Cách B - Lệnh / code deployment

```powershell
$SecretValue = @{ VNPAY_PAYMENT_URL=$env:VNPAY_PAYMENT_URL; VNPAY_TMN_CODE=$env:VNPAY_TMN_CODE; VNPAY_HASH_SECRET=$env:VNPAY_HASH_SECRET; AMB_ETHEREUM_ENDPOINT=$env:AMB_ETHEREUM_ENDPOINT } | ConvertTo-Json -Compress
aws secretsmanager create-secret `
  --name "medchain-ai/lab/integrations" `
  --secret-string $SecretValue `
  --region $Region `
  --profile $Profile
```

#### Kiểm tra

Describe secret nhưng không in ra giá trị nhạy cảm.
