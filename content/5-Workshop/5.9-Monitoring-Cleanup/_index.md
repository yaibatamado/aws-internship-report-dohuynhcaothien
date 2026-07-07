---
title : "Monitoring, security, cost, and cleanup"
date : 2024-01-01
weight : 9
chapter : false
pre : " <b> 5.9. </b> "
---

#### Monitoring

After the application has traffic, open CloudWatch to check logs and metrics.

#### Method A - AWS Console

1. Open **CloudWatch**.
2. Open **Log groups**.
3. Review Lambda log groups.
4. Open **Metrics** and check Lambda errors, duration and throttles.

![CloudWatch logs](/images/5-Workshop/5.9-Monitoring-Cleanup/log_group.png)
![CloudWatch logs](/images/5-Workshop/5.9-Monitoring-Cleanup/metric.png)

#### Method B - Command / code deployment

```powershell
aws logs describe-log-groups `
  --region $Region `
  --profile $Profile `
  --log-group-name-prefix "/aws/lambda" `
  --output table
```

#### Security and cost review

Check the following items:

+ Secrets are stored in Secrets Manager or environment variables, not hard-coded in frontend files.
+ S3 data bucket is not public.
+ API routes are protected by Cognito where required.
+ AMB node is deleted after the blockchain evidence screenshot is captured if the lab is no longer needed.
+ Billing dashboard is reviewed after deployment.


#### Cleanup order

Cleanup must be done in reverse order:

1. Stop using the web application.
2. Delete AMB Ethereum node.
3. Remove VNPay Sandbox IPN/Return URL if needed.
4. Disable and delete CloudFront distribution.
5. Empty S3 buckets.
6. Destroy CDK stack or delete CloudFormation stack.
7. Delete remaining Secrets Manager secrets if they were retained.
8. Check Billing and Cost Explorer.

```powershell
npx cdk destroy $StackName `
  --profile $Profile `
  --force
```
