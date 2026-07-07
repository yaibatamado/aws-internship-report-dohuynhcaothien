---
title : "Tổng quan workshop"
date : 2026-07-05
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---


#### Tình huống lab

Trong workshop này, bạn sẽ triển khai MedChain AI, một ứng dụng quản lý bệnh viện sử dụng AWS managed services cho frontend hosting, backend API, xác thực, database, thanh toán, blockchain validation và monitoring.

Sau khi hoàn thành lab, ứng dụng cần có:

+ Web frontend host trên Amazon S3 và phân phối bằng CloudFront.
+ Backend API mở bằng API Gateway và xử lý bằng Lambda.
+ Đăng nhập và phân quyền bằng Cognito.
+ Dữ liệu bệnh viện lưu trong DynamoDB và tài liệu lưu trong S3.
+ Luồng thanh toán hóa đơn bằng VNPay Sandbox.
+ Tích hợp AMB Ethereum node để lưu metadata toàn vẹn hồ sơ bệnh án.
+ CloudWatch logs, metrics và alarms.

![Tổng quan MedChain AI](/images/5-Workshop/5.1-Workshop-overview/mechain_ai.png)

#### Cách viết lab

Mỗi bước triển khai được viết theo hai cách:

+ **Cách A - AWS Console** dành cho người muốn thao tác trên giao diện AWS và chụp màn hình.
+ **Cách B - Lệnh / code deployment** dành cho người muốn triển khai lặp lại bằng AWS CLI, CDK và PowerShell.

Sử dụng stack name riêng cho lab:

```
MedChainAiLabStack
```
