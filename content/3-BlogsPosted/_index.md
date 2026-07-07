---
title: "Translated Blogs"
date: 2026-07-05
weight: 3
chapter: false
pre: " <b> 3. </b> "
---


This section introduces the AWS blog articles that were selected, translated, and summarized during the workshop. The selected blogs focus on practical cloud architecture topics such as data encryption, authentication experience, healthcare contact center modernization, AI/ML automation, security, compliance, and cost optimization on AWS.

Each translated blog presents a real-world technical problem and explains how AWS services can be used to solve it. Through these blogs, readers can better understand how cloud architecture is designed not only for functionality, but also for security, scalability, operational efficiency, user experience, and long-term cost control.

The first blog focuses on multi-tenant encryption using AWS KMS. The second blog discusses how Amazon Cognito and Authsignal can improve authentication experience through adaptive authentication. The third blog presents a healthcare case study showing how Amazon Connect and AWS AI/ML services can improve oncology patient support at scale.

### [Blog 1 - Simplify multi-tenant encryption with a cost-conscious AWS KMS key strategy](3.1-Blog1/)

This blog explains how to design a multi-tenant encryption strategy on AWS using AWS Key Management Service. It focuses on the challenge of protecting tenant data while controlling the cost and operational complexity of managing encryption keys.

Instead of creating a dedicated AWS KMS Customer Managed Key for every tenant, the article introduces a more flexible tiered key strategy. Enterprise or Premium tenants can use dedicated KMS keys for stronger isolation, while Standard or Free tenants can share KMS keys combined with Encryption Context for logical data separation.

The blog also discusses how Encryption Context helps prevent cross-tenant access, how dynamic access policies reduce manual configuration, and how AWS CloudTrail supports auditing and transparency. Overall, this blog provides a practical way to balance security, cost, scalability, and operational simplicity in SaaS systems.

### [Blog 2 - Creating great authentication experiences with Amazon Cognito and Authsignal](3.2-Blog2/)

This blog introduces how Amazon Cognito and Authsignal can work together to create a better authentication experience. The main idea is to balance strong security with a smooth user experience by using adaptive authentication, contextual risk signals, and step-up authentication.

The article explains that forcing users to complete MFA or OTP verification in every situation can create unnecessary friction. Instead, the system should evaluate the risk level of each login attempt or user action. Low-risk activities can continue with minimal friction, while suspicious or sensitive actions can require stronger authentication.

Amazon Cognito acts as the identity foundation by managing users, sign-in, and tokens. Authsignal adds a rules engine and risk-based decision layer that helps determine when additional authentication should be triggered. Together, they support flexible, secure, and user-friendly authentication flows.

### [Blog 3 - Scaling oncology patient support: How New York Cancer and Blood Specialists transformed customer experience with AWS and Pronetx, now part of Caylent](3.3-Blog3/)

This blog presents a healthcare case study about how New York Cancer and Blood Specialists improved its oncology patient support system using AWS and Pronetx, now part of Caylent. The article shows how a healthcare organization can modernize its contact center to handle a large number of patient calls more efficiently.

The solution uses Amazon Connect as the core cloud contact center platform. It also combines Amazon API Gateway, AWS Lambda, and Amazon DynamoDB to manage Contact Trace Records and disposition codes. For voicemail processing, recordings are stored in Amazon S3 and processed using Amazon Transcribe, helping convert patient voice messages into text and automatically create follow-up cases.

The blog also highlights the use of Amazon Lex and Amazon Polly for conversational AI and automated voice interactions. In addition, it discusses multilingual routing, queue prioritization, HIPAA-related security considerations, real-time monitoring, and structured deployment planning. Overall, this case study demonstrates how cloud contact center technology and AI/ML can improve patient support, reduce manual work, and enhance customer experience in healthcare.
