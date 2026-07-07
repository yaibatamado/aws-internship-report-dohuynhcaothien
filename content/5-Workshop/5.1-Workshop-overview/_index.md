---
title : "Workshop overview"
date : 2026-07-05
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---


#### Lab scenario

In this workshop, you will deploy MedChain AI, a hospital management application that uses AWS managed services for frontend hosting, backend API, authentication, database, payment integration, blockchain validation, and monitoring.

At the end of the lab, the application should include:

+ A web frontend hosted on Amazon S3 and delivered by CloudFront.
+ Backend APIs exposed by API Gateway and implemented by Lambda.
+ User sign-in and role groups managed by Cognito.
+ Hospital data stored in DynamoDB and documents stored in S3.
+ VNPay Sandbox payment flow for invoices.
+ AMB Ethereum node integration for medical record integrity metadata.
+ CloudWatch logs, metrics, and alarms.

![MedChain AI overview](/images/5-Workshop/5.1-Workshop-overview/mechain_ai.png)

#### Lab implementation pattern

Each deployment step is written with two methods:

+ **Method A - AWS Console** for learners who want to click through AWS services and capture screenshots.
+ **Method B - Command / code deployment** for learners who want repeatable deployment by AWS CLI, CDK, and PowerShell.

Use a separate lab stack name:

```
MedChainAiLabStack
```
