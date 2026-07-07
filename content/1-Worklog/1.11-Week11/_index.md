---
title: "Week 11 Worklog"
date: 2026-07-05
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives

* Build medical record, invoice, and payment screens on mobile.
* Integrate payment URL flow from the backend.
* Synchronize mobile data with backend and website behavior.

### Completed Work

| Item | Description |
| --- | --- |
| Medical records | Built screens showing the record ID based on citizen ID, patient information, visits, examination forms, prescriptions, lab results, and medical events. |
| Invoices | Built pending invoices, paid invoices, service fee details, and payment status screens. |
| Real payment | Integrated the flow for receiving `paymentUrl` from backend and opening VNPay/MoMo through webview or external browser. |
| Supporting screens | Added related screens such as lab results, invoice/cart, authorization, and missing pages so mobile is not only a static demo. |
| Flutter fixes | Fixed import, model, route, overflow, null-safety, missing `await`, and widget rebuild issues. |

### Outcomes

* Mobile includes backend-driven medical record and invoice screens.
* Real payment flow is prepared based on backend payment URLs.
* Endpoint names, data fields, and business statuses are aligned with backend/frontend teams.
