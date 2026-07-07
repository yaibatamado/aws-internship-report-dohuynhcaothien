---
title : "Workshop"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5. </b> "
---


# Triển khai MedChain AI trên AWS

#### Tổng quan

MedChain AI là bài lab thực hành xây dựng hệ thống quản lý bệnh viện hoàn chỉnh trên AWS. Workshop này hướng dẫn người học từ bước chuẩn bị đến khi ứng dụng chạy được trên CloudFront domain mặc định.

Bài lab có hai cách thực hiện:

+ **Cách A - AWS Console:** tạo và cấu hình tài nguyên bằng giao diện AWS Management Console.
+ **Cách B - Lệnh / code deployment:** tạo và triển khai tài nguyên bằng AWS CLI, AWS CDK, PowerShell và source code MedChain AI.

Website cuối cùng chạy bằng CloudFront distribution domain. VNPay Return URL và IPN URL cũng dùng CloudFront domain.

Thứ tự trong workshop được sắp xếp theo phụ thuộc thực tế: chuẩn bị tài khoản và công cụ, tạo các dịch vụ cần có trước khi deploy, triển khai stack ứng dụng, khởi tạo dữ liệu, cấu hình tích hợp, kiểm thử luồng nghiệp vụ, giám sát hệ thống và dọn dẹp tài nguyên.

#### Nội dung

1. [Tổng quan workshop](5.1-Workshop-overview/)
2. [Điều kiện chuẩn bị](5.2-Prerequisites/)
3. [Kiến trúc và thứ tự phụ thuộc](5.3-Architecture/)
4. [Nền tảng AWS](5.4-AWS-Foundation/)
5. [Dịch vụ chuẩn bị trước stack](5.5-Pre-Stack-Services/)
6. [Triển khai application stack](5.6-Deploy-Application/)
7. [Khởi tạo và chạy ứng dụng](5.7-Initialize-Run/)
8. [Cấu hình tích hợp và kiểm thử](5.8-Integration-Test/)
9. [Monitoring, bảo mật, chi phí và cleanup](5.9-Monitoring-Cleanup/)
