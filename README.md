# University Parking Permit & Appeals Service

System analysis, process redesign, and executable BPMN 2.0 architecture for the University Parking Permit & Appeals Service (CSC1016 Group 7, Project 2).

---

##  Project Overview

This repository contains the BPMN 2.0 process models, UML class structures, system designs, and HTML/CSS wireframes created to modernize a previously manual, paper-based university parking system. The system automates application validation, payment reconciliation, zone allocation, violation recording, appeals handling, and permit renewals while enforcing strict SLAs and business rules.

* **Course**: CSC1016


* **Team**: Group 7


* **Target Processing SLA**: $< 1$ working day (reduced from 5 days)


* **System Capacity**: Max 500 active permits



---

##  Team Members & Roles

| Member | Student ID | Project Role | Contribution

 |
| --- | --- | --- | --- |
| **Kiran Joseph** | `40699` | Project Lead & System Analyst | Scoped analysis, client liaison, process landscape & report drafting (25%)

 |
| **Andrey Pricop** | `18312` | BPMN Designer 1 | Models for Processes 1, 2, & 6; timers & event gateways (25%)

 |
| **Patrick Sebastian** | `21936` | BPMN Designer 2 & UI Lead | Models for Processes 3, 4, & 5; HTML/CSS wireframes (25%)

 |
| **Jake George** | `35982` | System Designer | UML class diagram, data models, model consistency & QA (25%)

 |

---

##  Core Processes (BPMN 2.0 Landscape)

The system models six interconnected end-to-end processes:

1. **Permit Application & Eligibility Verification**: Automated check for ID validity, unpaid fines, and active permits with interactive retry loops.


2. **Invoice Generation & Payment Processing**: Integration with the university finance system, enforcing 48-hour reminders and 5-day auto-cancellation via interrupting timer boundary events.


3. **Zone Allocation & Digital Permit Issuance**: Business rule classification (Staff $\rightarrow$ Zone A; Students $\rightarrow$ Zones B–D), bay assignment, and concurrent permit generation.


4. **Violation Detection & Fine Issuance**: Ground enforcement plate scanning, photographic evidence logging, compliance check, and auto-escalation for unregistered vehicles.


5. **Fine Appeal & Resolution**: 14-day submission window, weekly panel meeting schedule (7-day timer delay), 3-way decision routing (Cancel, Reduce, Uphold), and direct ledger updates.


6. **Permit Renewal & Expiry Management**: 30-day and 7-day automated reminders, eligibility re-verification, payment processing, or automatic account deactivation.



---

##  Business Rules & Design Highlights

* **Automated Deadlines**: Every SLA/deadline (48h payment, 5d cancellation, 14d appeal window, 30d expiry) is enforced natively by engine timers rather than manual tracking.


* **Priority Allocation**: Staff receive priority access to Zone A, while students are assigned across Zones B through D.


* **Single Sign-On (SSO)**: All user interactions authenticate against the core university SSO service.


* **Concurrency**: Parallel gateways handle digital permit ID generation and master database updates simultaneously.



---

##  Data Architecture (UML Model)

The data domain model includes the following primary entities:

* **`User`**: Base entity holding authentication and profile attributes.


* **`Application` & `Permit**`: Track state transitions during application, approval, and renewal.


* **`Zone` & `Bay**`: Enforce physical and system capacity limits ($N \le 500$).


* **`Invoice` & `Payment**`: Manage financial transaction status transitions (`Pending` $\rightarrow$ `Paid` / `Cancelled`).


* **`Violation` & `Fine**`: Record ground evidence and manage fine statuses (`Issued`, `Appealed`, `Paid`, `Cancelled`).


* **`Appeal` & `AppealsReviewer**`: Capture panel decisions and audit trails.



---

##  User Interface Wireframes

HTML/CSS mockups are located in the `UI Wireframes/` directory for high-traffic entry points:

* **`application_form.html`**: Process 1 user intake form.


* **`appeal_decision_form.html`**: Process 5 panel outcome decision form.


* **`renewal_form.html`**: Process 6 permit holder self-service renewal portal.



---

##  Repository Structure

```text
.
├── bpmn/                     # BPMN 2.0 XML/diagram export files
│   ├── process_1_application.bpmn
│   ├── process_2_payment.bpmn
│   ├── process_3_allocation.bpmn
│   ├── process_4_violation.bpmn
│   ├── process_5_appeals.bpmn
│   └── process_6_renewal.bpmn
├── uml/                      # UML class diagrams & data models
│   └── class_diagram.png
├── UI Wireframes/            # Standalone HTML/CSS wireframes
│   ├── application_form.html
│   ├── appeal_decision_form.html
│   └── renewal_form.html
├── docs/                     # Full project report and documentation
│   └── CSC1016_Report_Group_7.pdf
└── README.md

```
