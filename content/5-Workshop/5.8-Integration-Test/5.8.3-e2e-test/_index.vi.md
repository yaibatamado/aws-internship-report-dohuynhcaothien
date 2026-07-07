---
title : "Chạy kiểm thử end-to-end"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.8.3. </b> "
---

#### Mục tiêu

Chạy toàn bộ luồng bệnh viện sau khi đã cấu hình các tích hợp.

#### Cách A - AWS Console

1. Bệnh nhân đăng nhập và đặt lịch.
2. Nhân viên xác nhận lịch.
3. Bác sĩ tạo phiếu khám.
4. Hóa đơn được tạo.
5. Bệnh nhân thanh toán bằng VNPay Sandbox.
6. Metadata ledger của hồ sơ bệnh án được sinh ra.

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

#### Cách B - Lệnh / code deployment

```powershell
$AppDomain = "https://<cloudfront-domain>"
Invoke-WebRequest $AppDomain -UseBasicParsing
```

#### Kiểm tra

Ứng dụng cần hoàn thành luồng mà không có lỗi backend.
