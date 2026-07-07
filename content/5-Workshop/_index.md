---
title : "Workshop"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5. </b> "
---


# Deploy MedChain AI on AWS

#### Overview

MedChain AI is a hands-on lab for building a complete hospital management system on AWS. This workshop guides the learner from the preparation steps to a working application that can be opened from the default CloudFront domain.

The lab includes two implementation methods:

+ **Method A - AWS Console:** create and configure resources by using the AWS Management Console.
+ **Method B - Command / code deployment:** create and deploy resources by using AWS CLI, AWS CDK, PowerShell, and the MedChain AI source code.

The final website runs on the CloudFront distribution domain. VNPay Return URL and IPN URL also use the CloudFront domain.

The order in this workshop follows the real dependency order. You will prepare the account and tools first, create services that must exist before deployment, deploy the application stack, initialize application data, configure integrations, test the business flow, monitor the system, and clean up resources.

#### Content

1. [Workshop overview](5.1-Workshop-overview/)
2. [Prerequisites](5.2-Prerequisites/)
3. [Architecture and dependency order](5.3-Architecture/)
4. [AWS foundation](5.4-AWS-Foundation/)
5. [Pre-stack services](5.5-Pre-Stack-Services/)
6. [Deploy application stack](5.6-Deploy-Application/)
7. [Initialize and run the application](5.7-Initialize-Run/)
8. [Configure integrations and test](5.8-Integration-Test/)
9. [Monitoring, security, cost, and cleanup](5.9-Monitoring-Cleanup/)
