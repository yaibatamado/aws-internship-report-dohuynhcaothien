---
title : "Monitoring, bảo mật, chi phí và cleanup"
date : 2024-01-01
weight : 9
chapter : false
pre : " <b> 5.9. </b> "
---

#### Monitoring

Sau khi ứng dụng có traffic, mở CloudWatch để kiểm tra logs và metrics.

#### Cách A - AWS Console

1. Mở **CloudWatch**.
2. Mở **Log groups**.
3. Kiểm tra các Lambda log groups.
4. Mở **Metrics** và kiểm tra Lambda errors, duration và throttles.

![CloudWatch logs](/images/5-Workshop/5.9-Monitoring-Cleanup/log_group.png)
![CloudWatch logs](/images/5-Workshop/5.9-Monitoring-Cleanup/metric.png)

#### Cách B - Lệnh / code deployment

```powershell
aws logs describe-log-groups `
  --region $Region `
  --profile $Profile `
  --log-group-name-prefix "/aws/lambda" `
  --output table
```

#### Kiểm tra bảo mật và chi phí

Kiểm tra các mục sau:

+ Secrets được lưu trong Secrets Manager hoặc environment variables, không hard-code trong frontend files.
+ S3 data bucket không public.
+ API routes được bảo vệ bằng Cognito khi cần.
+ AMB node được xóa sau khi đã chụp bằng chứng blockchain nếu không còn dùng lab.
+ Billing dashboard được kiểm tra sau khi deploy.


#### Thứ tự cleanup

Cleanup phải thực hiện theo thứ tự ngược:

1. Ngừng sử dụng web application.
2. Xóa AMB Ethereum node.
3. Gỡ VNPay Sandbox IPN/Return URL nếu cần.
4. Disable và xóa CloudFront distribution.
5. Empty các S3 buckets.
6. Destroy CDK stack hoặc xóa CloudFormation stack.
7. Xóa Secrets Manager secrets còn lại nếu bị retain.
8. Kiểm tra Billing và Cost Explorer.

```powershell
npx cdk destroy $StackName `
  --profile $Profile `
  --force
```
