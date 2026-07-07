---
title : "Architecture and dependency order"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Architecture

The MedChain AI lab uses the following AWS services:

+ **CloudFront** to publish the website and forward `/api/*` requests.
+ **S3** to host frontend files and store medical documents.
+ **API Gateway** to expose backend APIs.
+ **Lambda** to run backend business logic.
+ **DynamoDB** to store application data.
+ **Cognito** to authenticate users and separate roles.
+ **Secrets Manager** to store integration configuration.
+ **Amazon Managed Blockchain Ethereum** to write real blockchain ledger proofs.
+ **CloudWatch** to monitor logs, metrics and errors.
+
+ **VNPay Sandbox** as the external payment gateway.

Users access the system through the CloudFront distribution domain.

![Sơ đồ kiến trúc](/images/5-Workshop/5.3-Architecture/architecture-0.png)

#### Main Execution Flow

1. The user sends an HTTPS request to the system via CloudFront.

2. CloudFront loads the static UI from S3 Frontend Static Content to return to the user.

3. When the frontend needs to process dynamic data, CloudFront forwards the API request to the API Gateway.

4. The API Gateway forwards the request to Lambda Core to process general system operations.

5. The API Gateway forwards the request to Lambda Medical Data to process operations related to medical data.

6. The API Gateway forwards the request to Lambda AI & Audit to process AI functionality or record audits.

7. The API Gateway forwards the request to Lambda Payment and SMS to process payments or send OTPs/SMS.

8. Lambda Core calls KMS to encrypt/decrypt data when needed.

9. Lambda Core retrieves the secret/API key from Secrets Manager for authentication or integration with external services.

10. Lambda Medical Data stores/retrieves medical records, documents, and images on S3.

11. Lambda Medical Data reads/writes business data on DynamoDB.

12. Lambda AI & Audit writes audit hash/transactions to the Amazon Managed Blockchain.

13. Lambda AI & Audit calls the Gemini API (Google) to implement AI Assistant functionality.

14. Lambda Payment and SMS pushes background tasks to SQS for asynchronous processing.

15. SQS triggers Lambda Trigger to process tasks in the queue.

16. Lambda Trigger sends a request to publish the OTP to the SNS.

17. The SNS sends the SMS OTP to the recipient.

18. Lambda Payment and SMS creates a payment request and sends it to the VNPay/MoMo payment gateway.

19. VNPay/MoMo sends a payment callback/IPN back to the API Gateway for the system to confirm and update the payment status.

#### Dependency order

The correct order is important because some resources depend on outputs from previous steps.

1. AWS account, budget, region and local profile.
2. CDK bootstrap resources.
3. VNPay Sandbox credentials.
4. AMB Ethereum node.
5. Secrets Manager configuration and environment variables.
6. CDK application stack.
7. DynamoDB, S3, Cognito, Lambda, API Gateway and CloudFront.
8. Dataset seed.
9. Frontend build and upload to S3.
10. CloudFront invalidation.
11. VNPay IPN and Return URL using CloudFront domain.
12. End-to-end testing and monitoring.
13. Cleanup in reverse order.

