---
title: "Blog 3"
date: 2026-07-05
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---


# Scaling oncology patient support: How New York Cancer and Blood Specialists transformed customer experience with AWS and Pronetx, now part of Caylent

In the healthcare industry, patient support is not only a customer service activity. It is also an important part of care delivery. When a patient contacts a healthcare provider, the speed and accuracy of the response can directly affect the patient experience and, in some cases, patient safety.

As healthcare organizations grow, managing a large number of patient calls manually becomes increasingly difficult. Staff may need to handle appointment requests, urgent questions, voicemail messages, language preferences, and specialist routing at the same time. If the call center is not designed well, patients may wait too long, calls may be routed incorrectly, and staff may become overloaded.

The AWS blog article **“Scaling oncology patient support: How New York Cancer and Blood Specialists transformed customer experience with AWS and Pronetx, now part of Caylent”** presents a real-world case study of how New York Cancer and Blood Specialists, also known as NYCBS, improved its patient support system using AWS cloud services.

NYCBS is a major oncology and hematology care provider in the United States. To improve its patient communication experience, NYCBS worked with AWS and Pronetx, now part of Caylent, to move from a legacy contact center model to a cloud-based contact center architecture using Amazon Connect.

The solution is not simply a phone system replacement. It combines cloud contact center technology, microservices, AI/ML services, automation, multilingual routing, and healthcare-grade security controls to improve call handling and patient support at scale.

## 1. The challenge of scaling patient support

Healthcare contact centers often face a very high volume of patient communication. Patients may call for many reasons, such as scheduling appointments, asking medical questions, following up on treatments, requesting prescription support, or leaving urgent voicemail messages after hours.

For oncology care providers, the situation can be even more sensitive. Cancer patients may need fast responses because delays can affect treatment coordination and patient confidence. A missed voicemail, slow callback, or incorrect routing can create stress for patients and extra workload for healthcare staff.

Before modernization, a traditional or multi-tenant contact center model may not provide enough flexibility. It can be difficult to customize workflows, integrate with healthcare systems, process voicemails automatically, or prioritize urgent cases. As call volume increases, manual processes become a bottleneck.

The article shows that NYCBS needed a more scalable and intelligent solution to support more than 250,000 calls per year and route patients across many different queues and specialties.

## 2. Using Amazon Connect as the core contact center platform

The central service in this architecture is **Amazon Connect**. Amazon Connect is a cloud-based contact center service that helps organizations build flexible customer service and communication workflows.

In the NYCBS case study, the organization moved from an older multi-tenant model to a dedicated Amazon Connect instance. This gave the healthcare provider more control, more flexibility, and better scalability.

The solution supports more than 100 queues for different specialties and patient support needs. These queues help route calls to the correct teams based on factors such as department, language, urgency, or service type.

Using Amazon Connect provides several advantages:

- Cloud-based contact center management
- Flexible call routing
- Integration with AWS services
- Support for automation and AI services
- Better scalability for high call volume
- Improved visibility into contact center operations

Instead of relying only on manual routing, the system can use automated flows and rules to direct calls more efficiently.

## 3. Microservices for Contact Trace Record management

Another important part of the architecture is the microservice used to manage **Contact Trace Records**, also known as CTRs. A Contact Trace Record contains details about a customer interaction, such as call status, routing information, duration, and disposition codes.

The system uses AWS services such as:

- Amazon API Gateway
- AWS Lambda
- Amazon DynamoDB

Amazon API Gateway exposes API endpoints for communication between components. AWS Lambda processes business logic without requiring server management. Amazon DynamoDB stores data such as disposition codes and related contact information for fast access.

This microservice-based approach makes the contact center system more flexible. Instead of putting all logic inside a single large application, each function can be handled by smaller cloud services. This improves scalability, maintainability, and integration with other systems.

For example, when a call ends, the system can record the call outcome, store the disposition code, and make that information available for reporting or follow-up workflows. This helps healthcare teams understand patient interactions more clearly.

## 4. AI/ML-powered voicemail processing

One of the most interesting parts of the solution is the AI/ML-powered voicemail workflow. In traditional contact centers, staff may need to listen to voicemail messages manually and type notes into a system. This process is time-consuming and can introduce human errors.

In the AWS-based architecture, voicemail recordings are stored securely in Amazon S3. When a new voicemail is uploaded, the system can trigger an automated processing workflow.

A simplified flow can be described as:

```text
Patient leaves voicemail
→ Recording is stored in Amazon S3
→ Amazon Transcribe converts speech to text
→ AWS Lambda processes the transcript
→ A case or task is created automatically
→ Staff can review and respond more quickly
```

Amazon Transcribe converts spoken audio into text. After the voicemail is transcribed, Lambda functions can process the text and create cases automatically. This reduces manual data entry and helps ensure that patient messages are not missed.

For healthcare support, this is very valuable. A patient who leaves a message after hours can have their voicemail converted into actionable information before staff manually review it. This improves continuity between shifts and allows the next team to respond faster.

## 5. Conversational AI with Amazon Lex and Amazon Polly

The architecture also uses conversational AI services such as **Amazon Lex** and **Amazon Polly**.

Amazon Lex helps build conversational interfaces and chatbots. It can understand natural language input and guide users through interactive flows. In a contact center environment, Lex can support automated call handling, self-service options, and intelligent routing.

Amazon Polly converts text into speech. This is useful for building voice responses in interactive voice response systems, also known as IVR. Instead of recording every message manually, the system can generate speech from text.

Together, Amazon Lex and Amazon Polly help improve the automation layer of the contact center.

Example use cases include:

- Greeting patients automatically
- Asking patients to select or describe their request
- Routing calls based on intent
- Providing automated responses
- Supporting common questions
- Reducing unnecessary workload for human agents

These services do not replace healthcare staff. Instead, they help handle repetitive interactions and allow staff to focus on more complex or urgent patient needs.

## 6. Multilingual routing and intelligent prioritization

Another important feature in the case study is multilingual routing. Patients may prefer to communicate in different languages. If a patient is routed to a team that cannot support their language, the experience becomes frustrating and inefficient.

The solution supports routing across multiple languages, including English, Spanish, Russian, and Mandarin. This helps patients reach the right support team more quickly.

The system also supports prioritization based on urgency. In healthcare, not all calls have the same level of importance. A general question may not require immediate attention, while an urgent oncology-related concern may need faster routing.

By using queue priority and routing rules, the system can help urgent cases reach the appropriate staff faster. This improves patient support and helps healthcare teams focus on the most critical interactions first.

A simplified routing idea can be shown as:

```text
Patient call received
→ Identify language and request type
→ Check urgency level
→ Route to the correct queue
→ Prioritize urgent cases
→ Connect patient to the right staff member
```

This type of intelligent routing is especially important in healthcare because patient communication is often time-sensitive.

## 7. Healthcare security and HIPAA considerations

Because the solution handles healthcare-related communication, security and compliance are critical. Healthcare systems may process sensitive information, including personal data and protected health information.

The article highlights the importance of a secure architecture that can support healthcare compliance requirements such as HIPAA. This means that data must be protected at every stage, including voice recordings, transcriptions, API calls, storage, and access management.

Important security practices include:

- Encrypting sensitive data
- Controlling access permissions carefully
- Managing secrets securely
- Monitoring system activity
- Protecting recordings and transcripts
- Using audit logs for compliance and investigation

AWS KMS can be used to encrypt data. AWS Secrets Manager can store sensitive configuration values securely. Access control and monitoring are also important to reduce the risk of unauthorized access.

In healthcare, a small mistake in permission configuration can lead to exposure of sensitive personal information. Therefore, cloud contact center systems must be designed with security from the beginning.

## 8. Real-time monitoring and call quality

A contact center must be monitored continuously. Even if the architecture is well designed, problems can still happen. For example, calls may be routed incorrectly, network quality may drop, or agents may experience poor audio quality.

The article mentions the need for real-time monitoring and third-party integrations such as Operata to track contact center performance and call quality.

Real-time monitoring helps teams detect issues early. It can provide visibility into:

- Call quality
- Queue performance
- Agent experience
- Connection problems
- Latency
- Failed or abandoned calls
- Routing issues

For healthcare providers, this monitoring is very important because communication problems can directly affect patient satisfaction and operational efficiency.

## 9. Deployment timeline and implementation process

The case study also shows that this type of transformation is not instant. The project required a structured implementation process that lasted about 13 weeks.

The process included phases such as:

- Discovery
- Architecture planning
- Build
- Integration
- Testing
- Acceptance testing
- Deployment

This is important because healthcare systems require careful planning and validation. A contact center migration cannot be treated as a simple plug-and-play replacement. The system must be tested to ensure that routing, security, voicemail processing, language support, and integrations work correctly.

A structured implementation process reduces the risk of service disruption and helps ensure that the final solution meets operational and compliance requirements.

![Blog 3](/images/3-Blog/Blog-3.png)

## 10. Main lessons from the article

The main lesson from this article is that a cloud contact center can do much more than receive and route phone calls. When combined with AWS services and AI/ML capabilities, it can become an intelligent patient support platform.

Important lessons include:

- Amazon Connect can serve as the core of a scalable cloud contact center.
- API Gateway, Lambda, and DynamoDB can support microservice-based contact record management.
- Amazon S3 and Amazon Transcribe can automate voicemail processing.
- Amazon Lex and Amazon Polly can improve conversational and IVR experiences.
- Multilingual routing improves accessibility for diverse patient groups.
- Priority queues help urgent healthcare cases receive faster attention.
- HIPAA-related security requirements must be considered from the beginning.
- Real-time monitoring is necessary to maintain call quality.
- Infrastructure as Code and CI/CD help support reliable deployment and future updates.

This case study shows how cloud services can improve both operational efficiency and patient experience.

## 11. Practical application

The ideas in this article can be applied to many healthcare and customer support organizations. Any organization that handles a large number of calls, voicemails, support requests, or urgent cases can benefit from a cloud-based contact center architecture.

In healthcare, this approach is especially useful because patient communication is often sensitive and time-critical. AI/ML automation can reduce administrative workload, but it must be implemented carefully with strong security controls.

For example, automatically transcribing voicemail messages can help staff respond faster. Intelligent routing can connect patients to the correct department. Multilingual support can improve accessibility. Queue prioritization can help urgent cases receive attention sooner.

However, automation should support human workers, not fully replace them. In healthcare, empathy, clinical judgment, and human review are still essential. The value of AI and cloud automation is that they reduce repetitive tasks and help staff focus on higher-value patient care activities.

## 12. Final thoughts

This article is useful because it shows how AWS services can transform a healthcare contact center into a scalable and intelligent patient support system. Amazon Connect provides the communication foundation, while services such as Lambda, API Gateway, DynamoDB, S3, Transcribe, Lex, and Polly add automation and intelligence.

The NYCBS case study demonstrates that cloud automation and AI/ML do not necessarily reduce empathy in healthcare. Instead, when designed correctly, they can remove repetitive administrative work and help healthcare staff respond to patients faster and more accurately.

At the same time, the article also reminds readers that healthcare automation requires careful planning. Security, compliance, monitoring, testing, and operational readiness are all essential. A successful solution must balance patient experience, technical reliability, and healthcare data protection.

## Original Article

AWS Architecture Blog:  
**Scaling oncology patient support: How New York Cancer and Blood Specialists transformed customer experience with AWS and Pronetx, now part of Caylent**

https://aws.amazon.com/vi/blogs/architecture/scaling-oncology-patient-support-how-new-york-cancer-and-blood-specialists-transformed-customer-experience-with-aws-and-pronetx-now-part-of-caylent/

## Discussion Question

What do you think about using AI/ML in healthcare contact centers and patient data workflows? Is HIPAA-related security one of the main reasons why many healthcare organizations are still cautious about adopting these technologies?