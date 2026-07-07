---
title : "Run end-to-end test"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.8.3. </b> "
---

#### Goal

Run the full hospital workflow after all integrations are configured.

#### Method A - AWS Console

1. Patient logs in and books an appointment.
2. Staff confirms the appointment.
3. Doctor creates examination record.
4. Invoice is created.
5. Patient pays with VNPay Sandbox.
6. Medical record ledger metadata is generated.

![End-to-end result](/images/5-Workshop/5.8-Integration-Test/5.8.3-e2e-test/dkl.png)
![End-to-end result](/images/5-Workshop/5.8-Integration-Test/5.8.3-e2e-test/dkl_completed.png)
![End-to-end result](/images/5-Workshop/5.8-Integration-Test/5.8.3-e2e-test/lk.png)
![End-to-end result](/images/5-Workshop/5.8-Integration-Test/5.8.3-e2e-test/ttlk.png)
![End-to-end result](/images/5-Workshop/5.8-Integration-Test/5.8.3-e2e-test/pk.png)
![End-to-end result](/images/5-Workshop/5.8-Integration-Test/5.8.3-e2e-test/pk_completed.png)
![End-to-end result](/images/5-Workshop/5.8-Integration-Test/5.8.3-e2e-test/dt.png)
![End-to-end result](/images/5-Workshop/5.8-Integration-Test/5.8.3-e2e-test/dt_completed.png)
![End-to-end result](/images/5-Workshop/5.8-Integration-Test/5.8.3-e2e-test/hsba.png)
![End-to-end result](/images/5-Workshop/5.8-Integration-Test/5.8.3-e2e-test/hsba_1.png)

#### Method B - Command / code deployment

```powershell
$AppDomain = "https://<cloudfront-domain>"
Invoke-WebRequest $AppDomain -UseBasicParsing
```

#### Validation

The application should complete the flow without backend errors.
