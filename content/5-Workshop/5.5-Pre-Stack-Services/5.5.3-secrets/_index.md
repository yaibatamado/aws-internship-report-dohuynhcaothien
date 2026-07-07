---
title : "Create Secrets Manager configuration"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.5.3. </b> "
---

#### Goal

Store integration settings before the application stack reads them.

#### Method A - AWS Console

1. Open **Secrets Manager**.
2. Store a new secret.
3. Add VNPay and AMB key-value pairs.
4. Name it `medchain-ai/lab/integrations`.

![Secrets created](/images/5-Workshop/5.5-Pre-Stack-Services/5.5.3-secrets/secrets.png)

#### Method B - Command / code deployment

```powershell
$SecretValue = @{ VNPAY_PAYMENT_URL=$env:VNPAY_PAYMENT_URL; VNPAY_TMN_CODE=$env:VNPAY_TMN_CODE; VNPAY_HASH_SECRET=$env:VNPAY_HASH_SECRET; AMB_ETHEREUM_ENDPOINT=$env:AMB_ETHEREUM_ENDPOINT } | ConvertTo-Json -Compress
aws secretsmanager create-secret `
  --name "medchain-ai/lab/integrations" `
  --secret-string $SecretValue `
  --region $Region `
  --profile $Profile
```

#### Validation

Describe the secret without printing sensitive values.
