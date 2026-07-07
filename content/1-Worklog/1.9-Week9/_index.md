---
title: "Week 9 Worklog"
date: 2026-07-05
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives

* Analyze the mobile application scope in SmartHospital P2TB.
* Design the Flutter project structure and AWS backend connection direction.
* Identify priority mobile screens.

### Completed Work

| Item | Description |
| --- | --- |
| Scope analysis | Identified mobile features: login, patient registration with citizen ID, home screen, appointment booking, medical records, prescriptions, lab results, invoices, and payment. |
| Flutter design | Planned folders for `screens`, `services`, `models`, `widgets`, `providers`, `theme`, and API client. |
| Authentication | Defined how mobile login works with Cognito/backend, secure token handling, authenticated API calls, and expired-session handling. |
| Initial UI | Designed UI direction aligned with the website: colors, headings, buttons, cards, forms, and loading/empty/error states. |
| Payment | Planned how to handle VNPay/MoMo `paymentUrl` on mobile through webview, external browser, or deeplink depending on the test environment. |

### Outcomes

* Finalized the mobile feature scope for the project phase.
* Prepared a clear Flutter structure for implementing the main screens.
* Defined the AWS backend integration and mobile payment flow direction.
