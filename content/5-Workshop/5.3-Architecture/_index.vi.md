---
title : "Kiến trúc và thứ tự phụ thuộc"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Kiến trúc

Bài lab MedChain AI sử dụng các dịch vụ AWS sau:

+ **CloudFront** để publish website và chuyển tiếp request `/api/*`.
+ **S3** để host frontend và lưu tài liệu y tế.
+ **API Gateway** để mở API backend.
+ **Lambda** để chạy logic nghiệp vụ backend.
+ **DynamoDB** để lưu dữ liệu ứng dụng.
+ **Cognito** để xác thực người dùng và phân quyền vai trò.
+ **Secrets Manager** để lưu cấu hình tích hợp.
+ **Amazon Managed Blockchain Ethereum** để ghi bằng chứng ledger blockchain thật.
+ **CloudWatch** để giám sát logs, metrics và lỗi.
+ **VNPay Sandbox** là cổng thanh toán bên ngoài.

Người dùng truy cập hệ thống bằng CloudFront distribution domain.

![Sơ đồ kiến trúc](/images/5-Workshop/5.3-Architecture/architecture-0.png)

#### Luồng thực thi chính

1. Người dùng gửi HTTPS request đến hệ thống thông qua CloudFront.

2. CloudFront tải giao diện tĩnh (static UI) từ S3 Frontend Static Content để trả về cho người dùng.

3. Khi frontend cần xử lý dữ liệu động, CloudFront sẽ forward API request đến API Gateway.

4. API Gateway chuyển request đến Lambda Core để xử lý các nghiệp vụ hệ thống chung.

5. API Gateway chuyển request đến Lambda Medical Data để xử lý các nghiệp vụ liên quan đến dữ liệu y tế.

6. API Gateway chuyển request đến Lambda AI & Audit để xử lý chức năng AI hoặc ghi nhận kiểm toán.

7. API Gateway chuyển request đến Lambda Payment and SMS để xử lý thanh toán hoặc gửi OTP/SMS.

8. Lambda Core gọi KMS để mã hóa/giải mã dữ liệu khi cần.

9. Lambda Core lấy secret / API key từ Secrets Manager để phục vụ xác thực hoặc tích hợp dịch vụ ngoài.

10. Lambda Medical Data thực hiện lưu trữ / truy xuất hồ sơ, tài liệu, hình ảnh y tế trên S3.

11. Lambda Medical Data thực hiện đọc / ghi dữ liệu nghiệp vụ trên DynamoDB.

12. Lambda AI & Audit ghi audit hash / transaction lên Amazon Managed Blockchain.

13. Lambda AI & Audit gọi Gemini API (Google) để thực hiện chức năng AI Assistant.

14. Labda Payment and SMS đẩy background task vào SQS để xử lý bất đồng bộ.

15. SQS kích hoạt Lambda Trigger để xử lý tác vụ trong hàng đợi.

16. Lambda Trigger gửi yêu cầu publish OTP đến SNS.

17. SNS gửi SMS OTP đến người dùng nhận OTP.

18. Lambda Payment and SMS tạo payment request và gửi sang cổng thanh toán VNPay/MoMo.

19. VNPay/MoMo gửi payment callback / IPN ngược về API Gateway để hệ thống xác nhận và cập nhật trạng thái thanh toán.

#### Thứ tự phụ thuộc

Thứ tự triển khai rất quan trọng vì một số tài nguyên cần output từ bước trước.

1. AWS account, budget, region và local profile.
2. CDK bootstrap resources.
3. VNPay Sandbox credentials.
4. AMB Ethereum node.
5. Secrets Manager configuration và environment variables.
6. CDK application stack.
7. DynamoDB, S3, Cognito, Lambda, API Gateway và CloudFront.
8. Seed dữ liệu mẫu.
9. Build frontend và upload lên S3.
10. CloudFront invalidation.
11. VNPay IPN và Return URL dùng CloudFront domain.
12. Kiểm thử end-to-end và monitoring.
13. Cleanup theo thứ tự ngược lại.

