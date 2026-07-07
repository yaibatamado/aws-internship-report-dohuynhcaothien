---
title: "Proposal"
date: 2026-07-05
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


# MedChain AI (AWS Serverless Hospital System Integrated with Blockchain, AI, and Real Payment)


### 1. Executive Summary

MedChain AI is a hospital system integrated with Blockchain and AI, built on the AWS platform to support digitalized hospital operations such as patient registration, appointment booking, doctor examination, medical record management, prescription creation, laboratory test management, invoice creation, and online payment. The system uses a serverless architecture to reduce infrastructure management, improve scalability, and fit the practical deployment scope of the project.

The platform uses Amazon Cognito for user authentication and authorization, AWS Lambda and API Gateway to build backend APIs, Amazon DynamoDB to store hospital data, Amazon S3 and Amazon CloudFront to deploy the frontend, and Amazon CloudWatch to record logs and support error checking. The web interface is developed using React/Vite and deployed as a static website.

An important function of MedChain AI is the Medical Integrity Ledger, which is used to verify the integrity of medical records. Important medical documents such as examination forms, prescriptions, laboratory test results, invoices, medical documents, and AI-generated medical summaries after being approved by doctors will be hashed and recorded in the ledger. The system is designed to use Amazon Managed Blockchain Access Ethereum to anchor medical record hashes to blockchain and store transaction evidence such as transactionHash, blockNumber, blockchainStatus, and confirmation time.

The AI component is used to support medical workflows, especially by helping summarize medical record information and allowing doctors to review patient history faster. AI-generated content is not considered a final medical conclusion. AI summaries must be reviewed and approved by doctors before being officially linked to the medical record.

In addition, the system integrates real payment through VNPay/MoMo. Patients can pay hospital invoices through a payment gateway, while the backend handles payment URL generation, return URL receiving, IPN/callback verification, transaction checking, invoice status updates, and payment history storage.

### 2. Problem Statement

#### Current Problems

Traditional hospital management processes often depend heavily on paperwork, manual operations, and data scattered across multiple departments. This can cause problems such as:

- Patient information, medical records, prescriptions, laboratory tests, and invoices are not synchronized.
- Patients find it difficult to book appointments, view medical records, or track payment status online.
- Doctors spend time looking up medical history and related medical documents.
- Medical staff need a centralized system to support appointments, laboratory tests, invoices, and hospital operations.
- Administrators need a secure platform to manage users, doctors, staff, patients, departments, services, medicines, news, and feedback.
- Medical records are sensitive data, so a mechanism is needed to check if data has been modified illegally.
- Payment needs to be linked with invoices and appointment status to complete the examination workflow.
- AI-generated content needs to be controlled and approved by doctors before official use.

#### Proposed Solution

MedChain AI proposes building an AWS serverless hospital system to centralize data and business workflows. Users access the system through the CloudFront domain. Amazon Cognito handles authentication and groups users into Admin, Doctor, Medical Staff, and Patient. After logging in, the frontend calls protected APIs through API Gateway, while AWS Lambda processes backend business logic.

DynamoDB is used as the main database following a single-table design model. The system stores data such as users, patients, doctors, medical staff, departments, appointments, medical records, examination forms, prescriptions, laboratory test results, invoices, payment transactions, news, feedback, AI summaries, and Medical Integrity Ledger blocks. Amazon S3 stores the static frontend and can be extended to store medical documents or uploaded files. CloudWatch supports Lambda logging and error checking during deployment.

For medical record management, MedChain AI uses CCCD as the main medical record ID. This helps each patient have a consistent record and reduces duplicate or incorrect data. Examination forms, prescriptions, laboratory test results, invoices, and approved AI summaries are all linked to the same medical record ID.

For blockchain, the system generates SHA-256 hashes for important medical documents and records them in the Medical Integrity Ledger. When AMB is enabled, selected hashes will be anchored to Ethereum through Amazon Managed Blockchain Access Ethereum. Only hashes and minimal metadata are sent to blockchain. Real medical record data is still stored in DynamoDB or S3.

For AI, the system supports generating medical record summaries to help doctors review patient history faster. AI summaries need to be approved by doctors before becoming an official part of the medical record.

For real payment, the system integrates VNPay/MoMo. The backend creates payment requests, redirects patients to the payment gateway, verifies returned callbacks or IPNs, updates invoice status, stores transaction codes, and records payment history.

#### Benefits and Return on Investment

MedChain AI helps digitize hospital processes and reduce dependence on manual operations. Patients can book appointments, view medical records, track invoices, and pay online. Doctors can view medical history, create examination forms, prescribe medicine, request laboratory tests, and approve AI summaries. Medical staff can support testing, invoicing, and operational workflows. Administrators can manage system data and user accounts from a centralized interface.

Technically, the project helps practice many important AWS components such as serverless architecture, secure authentication, API development, NoSQL data modeling, frontend deployment, real payment integration, AI support in medical workflows, and data integrity verification using blockchain.

The blockchain component helps increase the reliability of medical data by storing hashes of important records. If data is modified directly in the database without going through the system workflow, the system can recalculate the hash and compare it with the value stored in the ledger to detect unauthorized changes.

The AI component helps improve the efficiency of medical record information processing, but doctors remain the final approvers to ensure medical safety and responsibility.

Real payment integration makes the system closer to a practical hospital model because invoices are linked with payment transactions, verified callbacks, and payment status.

### 3. Solution Architecture

MedChain AI uses an AWS serverless architecture. The frontend is built with React/Vite and deployed to Amazon S3 as static files. Amazon CloudFront distributes the website through HTTPS and improves access speed. Users log in using Amazon Cognito. After logging in, the frontend sends requests with JWT tokens to API Gateway. API Gateway forwards requests to AWS Lambda functions, and Lambda then reads or writes data to DynamoDB.

DynamoDB stores the main hospital data using a single-table design model. The system also stores Medical Integrity Ledger blocks in DynamoDB and stores blockchain transaction information after anchoring hashes through Amazon Managed Blockchain. AWS Secrets Manager is used to store sensitive configurations such as payment information, AMB RPC endpoint, and private key. CloudWatch is used to record backend logs and support error checking.

The AI flow is processed through the backend service. Medical data is retrieved from DynamoDB, processed into a safe summary, and then reviewed and approved by doctors before being saved into the official medical record. Approved AI summaries can also be added to the Medical Integrity Ledger for integrity verification.

![MedChain AI AWS Architecture](/images/2-Proposal/architecture.png)


#### AWS Services Used

- **Amazon Cognito**: Manages user authentication and role-based authorization for Admin, Doctor, Medical Staff, and Patient.
- **Amazon API Gateway / HTTP API**: Provides secure API endpoints for the frontend.
- **AWS Lambda**: Processes backend business logic such as users, appointments, medical records, prescriptions, laboratory tests, invoices, payments, AI summaries, and ledger verification.
- **Amazon DynamoDB**: Stores hospital data using a single-table design model.
- **Amazon S3**: Stores the static frontend and medical documents or uploaded files.
- **Amazon CloudFront**: Distributes the frontend website through HTTPS and caching.
- **Amazon CloudWatch**: Records logs, supports monitoring, error checking, and system verification.
- **AWS Secrets Manager**: Stores sensitive configurations such as VNPay/MoMo information, AMB endpoint, and blockchain private key.
- **Amazon Managed Blockchain Access Ethereum**: Anchors medical record hashes to Ethereum and provides blockchain transaction evidence.
- **AI Processing Module**: Supports creating medical record summaries and requires doctor approval before official storage.
- **VNPay/MoMo Payment Gateway**: Processes real invoice payments through an external payment gateway.
- **AWS Root/Admin Account**: Used as the highest-level administrator account to create, deploy, and manage all AWS resources in the workshop environment.

#### Component Design

- **Frontend Application**: A React/Vite application with separate interfaces for Admin, Doctor, Medical Staff, and Patient.
- **Authentication Layer**: Amazon Cognito authenticates users and groups them by role.
- **API Layer**: API Gateway receives requests from the frontend and forwards them to the corresponding Lambda functions.
- **Business Logic Layer**: AWS Lambda processes appointment booking, examination, prescription, laboratory test, invoice, payment, AI summary approval, and ledger verification.
- **Data Layer**: DynamoDB stores structured hospital data, and S3 stores the static frontend and medical documents.
- **AI Layer**: Creates medical record summaries from medical data and requires doctor approval before official storage.
- **Payment Layer**: VNPay/MoMo handles payment request creation, return URL, IPN/callback verification, and invoice updates.
- **Medical Integrity Ledger**: Creates hashes for important medical documents and stores ledger blocks.
- **Blockchain Anchoring Layer**: Amazon Managed Blockchain Access Ethereum anchors selected hashes to Ethereum and stores transactionHash, blockNumber, and blockchainStatus.
- **Monitoring Layer**: CloudWatch Logs helps check API errors, Lambda execution results, and integration issues.

### 4. Technical Implementation

#### Implementation Phases

The project is implemented through four main phases:

1. **Requirement Analysis and Architecture Design**  
   Analyze hospital business workflows, identify user roles, design the AWS architecture, and select the services required for authentication, APIs, data storage, frontend hosting, AI support, payment, and blockchain.

2. **Building AWS Infrastructure and Core Backend**  
   Use AWS CDK to deploy Cognito, API Gateway, Lambda, DynamoDB, S3, CloudFront, IAM Role, CloudWatch Logs, and environment configurations. Develop the first APIs for user profiles, patients, doctors, appointments, and medical records.

3. **Completing Medical, AI, Payment, and Blockchain Workflows**  
   Implement the medical record workflow, standardize CCCD as the main medical record ID, build the Medical Integrity Ledger, design hash anchoring to AMB, support AI summary generation, and integrate the real VNPay/MoMo payment flow.

4. **Testing, Deployment, and Final Verification**  
   Deploy backend and frontend, seed and verify the dataset, test user authorization, check medical record display, check AI summary approval, verify the ledger, test payment callbacks, and prepare final documentation.

#### Technical Requirements

- **Frontend**: React, Vite, Axios, role-based routing, responsive interface.
- **Backend**: Node.js Lambda, AWS SDK, API Gateway integration.
- **Authentication**: Amazon Cognito User Pool, JWT token, Cognito groups.
- **Database**: DynamoDB single-table design with partition key and sort key.
- **Storage**: S3 for static frontend and medical documents.
- **Content Delivery**: CloudFront for frontend access.
- **Deployment**: AWS CDK, AWS CLI, PowerShell scripts, S3 sync, CloudFront invalidation.
- **AI**: Creates medical record summaries with a doctor approval mechanism.
- **Payment**: VNPay/MoMo payment flow with return URL and IPN/callback.
- **Blockchain**: Medical Integrity Ledger and AMB Access Ethereum.
- **Security**: IAM Role, Secrets Manager, Cognito authorization, and the principle of least privilege.
- **Monitoring**: CloudWatch Logs for Lambda debugging and system verification.

### 5. Timeline & Milestones

- **Week 1 - Planning and Architecture Design**  
  Analyze project requirements, identify hospital workflows, design the AWS architecture, and plan user roles, database, AI, payment, and blockchain.

- **Week 2 - Infrastructure and Core System Setup**  
  Deploy AWS infrastructure with CDK, configure Cognito, API Gateway, Lambda, DynamoDB, S3, CloudFront, and deploy the frontend to AWS.

- **Week 3 - Medical Records, AI, Payment, and Blockchain**  
  Standardize medical records by CCCD, build the Medical Integrity Ledger, design AMB transaction anchoring, prepare AI summary support, and implement the VNPay/MoMo payment flow.

- **Week 4 - Testing and Finalization**  
  Test the production deployment, reset and verify the dataset, backfill the ledger, check blockchain validation, review AI summary approval, test payment callbacks, and complete documentation.

### 6. Budget Estimation

The final cost depends on the number of requests, data storage volume, CloudFront traffic, AI usage, number of payment tests, and AMB usage level. Costs should be checked again using AWS Pricing Calculator before official deployment.

#### Infrastructure Costs

- **AWS Lambda**: Depends on the number of requests and execution time.
- **API Gateway / HTTP API**: Depends on the number of API requests.
- **DynamoDB**: Depends on storage volume and the number of read/write requests.
- **Amazon S3**: Depends on frontend storage, medical documents, and number of requests.
- **Amazon CloudFront**: Depends on data transfer and number of requests.
- **Amazon Cognito**: Suitable for a small number of users within the demo scope.
- **CloudWatch Logs**: Depends on log volume and log retention period.
- **Secrets Manager**: Incurs cost if secrets for payment and blockchain are stored.
- **Amazon Managed Blockchain**: May incur costs if using Ethereum Mainnet node, token accessor, or many requests.
- **AI Processing**: Depends on the AI provider, number of requests, and amount of medical text processed.
- **VNPay/MoMo**: Sandbox testing usually does not incur transaction fees, while real payment depends on merchant configuration and provider policies.

Within the project scope, the system should use a small dataset, a limited number of accounts, short log retention, controlled AI usage, and careful AMB usage control. If Ethereum Mainnet is used, the team needs to monitor request costs and possible gas fees.

### 7. Risk Assessment

#### Risk Matrix

- **Medical record inconsistency**: High impact, medium probability.  
  Modules may use different medical record IDs if CCCD is not standardized.

- **Incorrect user authorization**: High impact, medium probability.  
  Users may access data outside their role if the backend does not fully check permissions.

- **AI content risk**: High impact, medium probability.  
  AI summaries may be incomplete or inaccurate if they are not reviewed by doctors.

- **Payment callback error**: High impact, medium probability.  
  Invoice status may not update correctly if return URL or IPN verification fails.

- **Blockchain verification error**: Medium impact, medium probability.  
  The ledger may become invalid if the dataset is reset but the ledger is not cleared and backfilled again.

- **Sensitive data exposure**: High impact, low probability.  
  Real medical record data must not be stored directly on blockchain or returned through public APIs.

- **AWS cost overrun**: Medium impact, medium probability.  
  AMB, CloudWatch Logs, CloudFront, AI usage, WAF, and Ethereum transactions may create unexpected costs.

#### Mitigation Strategies

- Use CCCD as the unique medical record ID.
- Apply Cognito groups and check permissions in the backend.
- Store sensitive information in AWS Secrets Manager.
- Do not store real medical record data directly on Ethereum.
- Require doctors to approve AI summaries before saving them into official medical records.
- Verify VNPay/MoMo signatures and payment amounts before updating invoices.
- Clear and recreate the ledger after resetting the dataset.
- Use CloudWatch Logs to check errors and set a reasonable log retention period.
- Set up AWS Budget alerts to monitor costs.

#### Contingency Plans

- If real payment is not available yet, use VNPay/MoMo sandbox for testing while keeping the correct real payment flow structure.
- If AMB cost is too high, keep the Medical Integrity Ledger in DynamoDB and enable AMB only for selected demonstration transactions.
- If AI results are not reliable, limit AI to draft mode and require doctor approval.
- If CloudFront still displays the old frontend version, perform invalidation and clear browser cache.
- If the dataset is incorrect, reset and verify the dataset using scripts.
- If blockchain validation reports invalid after reset, delete the old ledger and run ledger backfill again.

### 8. Expected Outcomes

#### Technical Improvements

The project is expected to build a complete AWS serverless hospital system with user authentication, role-based authorization, medical record management, appointment booking, prescriptions, laboratory tests, invoices, real payment, AI medical record summaries, and medical record integrity verification.

The system demonstrates how multiple AWS services can be combined to build a practical healthcare application. At the same time, the project shows how blockchain can be used appropriately by storing only hashes and metadata, without storing sensitive medical record data directly on blockchain. AI is used to support doctors, not to replace medical decisions.

#### Long-term Value

MedChain AI can be expanded into a more complete hospital system in the future. Future development directions include full VNPay/MoMo production integration, improved AI medical record summaries, medical suggestion support for doctors, SMS/email notifications, data analytics dashboards, mobile app integration, and stronger blockchain anchoring with smart contracts.