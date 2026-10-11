# MVP Requirements: Cargo Handling and Doorstep Collection Management System

## 1. Document Information

| Field | Value |
|---|---|
| Document title | MVP Requirements: Cargo Handling and Doorstep Collection Management System |
| Version | 0.1 - Initial proposal |
| Status | Draft - Pending Business Review |
| Issue reference | GitHub Issue #1 - Define MVP Requirements and User Roles |
| Project/repository name | MyFirstProfessionalApp (provided in the request; relationship to the CargoTracking workspace is To Be Confirmed) |
| Prepared for | Business and project stakeholders |
| Date | 10 October 2026 |

### Requirement status terminology

- **Proposed** identifies an initial recommendation that has not been approved as a business rule.
- **To Be Confirmed (TBC)** identifies a decision or detail that stakeholders must supply.
- The technology stack and issue reference above are recorded as provided project context. The operational requirements in this document are proposals unless specifically stated otherwise.

## 2. Project Overview

The proposed system will support the management of doorstep collection requests and the registration and operational tracking of cargo. Its intended users include requesters and operational staff. The system should make request progress, collection outcomes, cargo events, and exceptions traceable.

The supplied technology context is Angular with TypeScript for the frontend, ASP.NET Core Web API for the backend, Microsoft SQL Server for the database, and Clean Architecture for the application architecture. These are project context, not additional functional requirements.

The system must not treat a scheduled or attempted collection as a successful collection, nor treat collected or registered cargo as automatically accepted. The business meaning and transitions for these states remain **To Be Confirmed**.

## 3. Business Objectives

The following objectives are **Proposed** and require business review:

- Provide a consistent process for submitting and managing doorstep collection requests.
- Give operations staff visibility into requests, assignments, collection outcomes, cargo progress, and unresolved exceptions.
- Maintain a traceable history of request and cargo events.
- Make failed attempts, cancellations, rescheduling, cargo holds, and other agreed exceptions visible for follow-up.
- Reduce reliance on disconnected channels and manually maintained records where the system can support the approved process.

Specific business targets, service levels, cost savings, throughput goals, or customer-satisfaction measures are **To Be Confirmed**. No operational metric is assumed by this document.

## 4. Proposed User Roles

All roles and responsibilities below are **Proposed**. Role boundaries, eligibility, and permissions are **To Be Confirmed**.

| Proposed role | Proposed responsibilities |
|---|---|
| Customer / Requester | Submit a collection request, provide required details, view permitted request status, and request cancellation or rescheduling where allowed. |
| Dispatcher / Operations Coordinator | Review requests, coordinate scheduling and assignment, manage request changes, and monitor work and exceptions. |
| Collection Agent | View assigned collections, record attempts and outcomes, and report handover details or issues. |
| Cargo Handling Operator | Register cargo when authorized by the business process, record handling or movement events, and report discrepancies or holds. |
| Operations Manager | Monitor operational queues and exceptions, review operational records and reports, and oversee operational users as authorized. |
| System Administrator | Administer system access and technical configuration. Business configuration permissions should be distinguished from technical administration. |

Whether requesters are external customers, internal staff, or both is **To Be Confirmed**. Authentication method, user provisioning, and detailed permission matrices are also **To Be Confirmed**.

## 5. MVP Scope

The proposed MVP includes:

- Identity and role-based access for the user groups approved for the MVP.
- Collection request creation, review, status visibility, and permitted changes.
- Scheduling and assignment recording, subject to business-approved operating rules.
- Recording collection attempts and their outcomes, including unsuccessful attempts.
- Cargo registration and explicit recording of acceptance or other disposition decisions where applicable.
- Cargo operational event history and exception visibility.
- Notifications for business-approved events, if notification delivery is confirmed as an MVP need.
- Basic operational work queues and audit history.

Detailed inclusion depends on confirmation of user groups, process states, data requirements, operational rules, and integrations. The scope is not a commitment to automated dispatch, real-time tracking, or any service level.

## 6. Functional Requirements

All requirements in this section are **Proposed**. Any business rule, field, state transition, or permission not specified here is **To Be Confirmed** before implementation.

### Collection request management

- **FR-001 (Proposed):** The system shall allow an authorized requester or staff member, according to the approved access model, to submit a collection request and receive a traceable reference.
- **FR-002 (Proposed):** The system shall validate request data against the required fields and validation rules approved by the business.
- **FR-003 (Proposed):** The system shall allow authorized users to review a request and record its business-approved next state, including a request for clarification or a decision not to proceed if those outcomes are approved.
- **FR-004 (Proposed):** The system shall allow authorized users to record permitted request changes, cancellations, and rescheduling while preserving the prior request history.
- **FR-005 (Proposed):** The system shall allow authorized users to find requests using business-approved identifiers and filters.

### Scheduling, assignment, and collection execution

- **FR-006 (Proposed):** The system shall allow authorized operations users to record and revise planned collection details and assignment information.
- **FR-007 (Proposed):** The system shall allow an authorized collection agent to view the agent's assigned collection work, subject to the approved access model.
- **FR-008 (Proposed):** The system shall allow an authorized collection agent or operations user to record each collection attempt and its outcome.
- **FR-009 (Proposed):** The system shall represent a failed attempt separately from a successful handover and shall not mark a request complete solely because it was scheduled or attempted.
- **FR-010 (Proposed):** The system shall record the actor and time associated with an attempt and any required outcome details approved by the business.

### Cargo registration and tracking

- **FR-011 (Proposed):** The system shall allow an authorized user to register cargo using the identifiers and attributes approved by the business.
- **FR-012 (Proposed):** The system shall represent cargo registration separately from cargo acceptance when the business defines them as separate decisions.
- **FR-013 (Proposed):** The system shall allow authorized users to record approved cargo handling, custody, location, status, and exception events.
- **FR-014 (Proposed):** The system shall provide authorized users with the recorded event history for a cargo record.
- **FR-015 (Proposed):** The system shall prevent or flag status transitions that conflict with the business-approved transition rules.
- **FR-016 (Proposed):** The system shall support linking cargo to its applicable collection request or other approved reference.

### Notifications, audit, and operational views

- **FR-017 (Proposed):** The system should notify approved recipients about business-approved events through business-approved channels. Recipients, channels, content, and delivery behavior are **To Be Confirmed**.
- **FR-018 (Proposed):** The system shall preserve a history of significant request, cargo, assignment, and permission changes, including actor and timestamp where applicable.
- **FR-019 (Proposed):** The system shall provide authorized users with operational views of work and exceptions using business-approved status definitions and filters.
- **FR-020 (Proposed):** The system shall report a failed save or update clearly and shall not present an unpersisted change as successful.

## 7. Doorstep Collection Workflow

This workflow is **Proposed**. The states, decision authority, required fields, and timing rules are **To Be Confirmed**.

1. **Request submission:** An authorized requester supplies the information required by the approved process. The system assigns or records a traceable request reference.
2. **Review:** An authorized operations user reviews the request and records an approved decision, such as proceeding, requesting clarification, or not proceeding, if those outcomes are adopted.
3. **Scheduling and assignment:** If the request proceeds, an authorized operations user records the planned collection details and assignment. Availability, capacity, route, and scheduling rules are **To Be Confirmed**.
4. **Attempt:** The assigned agent records that an attempt occurred and selects or enters an approved outcome.
5. **Outcome handling:**
   - For a successful handover, record the handover details and any evidence required by the approved process.
   - For an unsuccessful attempt, record the failure outcome and required details; leave the request in an appropriate follow-up state rather than treating it as successful.
   - For a partial or disputed outcome, use a distinct outcome only if the business defines its meaning and handling.
6. **Cancellation or rescheduling:** An authorized party records the requested or completed change, its time, and resulting state. Who may request or approve changes and at what stage is **To Be Confirmed**.
7. **Completion:** The request is completed only when the business-approved completion conditions are met. Collection-request completion and later cargo acceptance or delivery milestones shall not be conflated.

## 8. Cargo Registration and Tracking Workflow

This workflow is **Proposed**. Cargo identification, acceptance authority, custody events, and lifecycle completion rules are **To Be Confirmed**.

1. **Identify cargo:** Record the identifiers and details required by the approved process. Identifier generation and uniqueness rules are **To Be Confirmed**.
2. **Record registration:** An authorized user registers the cargo and links it to the relevant request or other approved reference.
3. **Record disposition:** Record the applicable business decision, such as pending review, accepted, refused, or another approved disposition. A collection or registration event alone shall not imply acceptance.
4. **Track operations:** Authorized users record approved handling, custody, location, status, and exception events with the required actor and time information.
5. **Resolve exceptions:** Record follow-up and resolution as additional events; do not erase the original exception history.
6. **Complete lifecycle:** Close or conclude cargo tracking only according to business-approved terminal outcomes, which may include delivery, return, refusal, or another defined result if included in scope.

The business must define whether *collected*, *received into custody*, *registered*, and *accepted* are distinct states and what evidence or authority is required for each.

## 9. Exception and Failure Scenarios

The system should support the following scenarios as distinct recorded outcomes where applicable. Exact state names, decision rights, reason codes, and next actions are **To Be Confirmed**.

| Scenario | Proposed system behavior | Decisions to confirm |
|---|---|---|
| Collection unsuccessful | Record the attempt and unsuccessful outcome; do not mark collection successful. | Approved failure reasons, required details, retry and follow-up process. |
| Request cancellation | Record the cancellation request or decision, actor, time, and resulting request state. | Who may cancel, approval needs, and stages at which cancellation is allowed. |
| Rescheduling | Record the schedule change and retain the previous schedule in history. | Who may request/approve the change, permissible timing, and notifications. |
| Request needs clarification | Preserve the request and record that information or action is pending, if adopted. | Clarification workflow, responsible party, and closure rules. |
| Cargo not accepted or acceptance pending | Record the decision separately from collection and registration. | Decision authority, allowed dispositions, reason requirements, and next steps. |
| Cargo discrepancy, damage, or hold | Record an exception and any approved follow-up or resolution event. | Which exception types are in scope and what data or evidence is required. |
| Partial or disputed handover | Do not infer full success; record a distinct outcome only if defined. | Whether this scenario can occur and how cargo quantities and request states are handled. |
| Save or service failure | Clearly report the failure and avoid indicating that an unpersisted change succeeded. | Retry, duplicate-submission, and reconciliation behavior. |

## 10. Non-Functional Requirements

The requirements below are **Proposed**. Numeric targets, applicable policies, and verification thresholds are **To Be Confirmed**; this document does not invent service commitments or operational metrics.

### Security

- **NFR-001 (Proposed):** The system shall authenticate users through an approved identity mechanism and enforce authorization according to the approved role and permission model.
- **NFR-002 (Proposed):** The system shall restrict access to personal, cargo, operational, and administrative data according to approved access rules and least-privilege principles.
- **NFR-003 (Proposed):** The system shall protect data in transit and at rest using approved platform capabilities and shall manage secrets without embedding them in application source.
- **NFR-004 (Proposed):** The system shall validate input and protect privileged administrative functions. Security verification criteria and applicable organizational policies are **To Be Confirmed**.

### Auditability and data integrity

- **NFR-005 (Proposed):** The system shall record significant business and administrative changes with the actor, timestamp, affected record, and change details as defined by the audit policy.
- **NFR-006 (Proposed):** The system shall preserve the event history needed to review request and cargo state changes; access, retention, and tamper-resistance requirements are **To Be Confirmed**.
- **NFR-007 (Proposed):** The system shall maintain consistent identifiers and approved record relationships and shall handle duplicate or conflicting updates according to rules **To Be Confirmed**.

### Performance and reliability

- **NFR-008 (Proposed):** The system shall meet response-time targets for agreed key workflows under agreed load and data-volume test conditions. Targets and test conditions are **To Be Confirmed**.
- **NFR-009 (Proposed):** The system shall meet availability, backup, and recovery objectives approved by the business and technical owners. Objectives and support responsibilities are **To Be Confirmed**.
- **NFR-010 (Proposed):** The system shall handle transient failures without silently losing or duplicating persisted business events. Retry and reconciliation behavior is **To Be Confirmed**.

### Usability, compatibility, and operations

- **NFR-011 (Proposed):** The user interface shall present clear status labels, validation feedback, and exception states appropriate to the user's authorized tasks.
- **NFR-012 (Proposed):** The system shall meet accessibility, browser, device, localization, and time-zone requirements approved for the MVP; the required standards and support matrix are **To Be Confirmed**.
- **NFR-013 (Proposed):** The system shall expose operational logs and health information sufficient to investigate failures without unnecessarily exposing sensitive data.
- **NFR-014 (Proposed):** The system shall handle personal data according to organizationally approved purpose, access, retention, and deletion rules. Applicable obligations and rules are **To Be Confirmed** by the organization.

## 11. Acceptance Criteria

The following criteria are **Proposed** and are intended to be testable against business-approved roles, fields, states, and test data. They do not establish service-level targets.

- **AC-001:** Given a user authorized to submit a request and request data satisfying the approved required fields, when the user submits it, then the system stores the request and displays a traceable request reference.
- **AC-002:** Given a request with one or more approved missing or invalid fields, when an authorized user attempts submission, then the system identifies the validation failure and does not record the request as successfully submitted.
- **AC-003:** Given a request that operations has scheduled and assigned, when an authorized agent records an unsuccessful attempt, then the system records the attempt and its outcome, and the request is not represented as successfully collected solely because of that attempt.
- **AC-004:** Given an existing request, when an authorized user records a cancellation or rescheduling, then the system shows the resulting state and retains the prior request or schedule history with the actor and time.
- **AC-005:** Given a successful handover, when an authorized user records it, then the system records a handover outcome separately from cargo acceptance whenever the approved process defines those as distinct decisions.
- **AC-006:** Given cargo that has been collected or registered but has no recorded acceptance decision, when an authorized user views its disposition, then the system does not show it as accepted by implication.
- **AC-007:** Given cargo linked to a request, when an authorized user records an approved cargo event, then the system stores the event and authorized users can view it in the cargo event history.
- **AC-008:** Given a recorded exception, when an authorized user records follow-up or resolution, then the system retains both the original exception and the later event in the record history.
- **AC-009:** Given a user without permission for a restricted operation, when that user attempts the operation, then the system denies the operation and does not persist the restricted change.
- **AC-010:** Given a failed save or update, when the operation cannot be persisted, then the system reports failure and does not show the unpersisted change as successful.
- **AC-011:** Given significant request, cargo, assignment, or permission changes, when an authorized reviewer opens the applicable history, then each configured auditable change displays the required actor, timestamp, affected record, and change details.
- **AC-012:** Given approved operational queue definitions and records in each included state, when an authorized operations user opens the corresponding view, then each record appears according to the approved filters and state definitions.
- **AC-013:** Given approved workload and response-time targets, when the agreed performance test is run using the agreed test conditions, then results are measured and assessed against those targets. The targets and test conditions must be agreed before this criterion can pass.

## 12. Out-of-Scope Features

The following are **Proposed exclusions** from the MVP unless stakeholders explicitly approve otherwise:

- Route optimization, automated dispatch, and predictive scheduling.
- Real-time vehicle or driver tracking.
- Billing, pricing, payment processing, and invoicing.
- Warehouse inventory management, packing, and advanced sorting.
- Customs, regulatory, or dangerous-goods decision automation.
- Advanced proof-of-delivery workflows beyond evidence explicitly required for the approved collection or handover process.
- A full customer self-service portal beyond any request submission and basic status visibility approved for MVP.
- Advanced analytics, forecasting, and configurable business intelligence.
- Automated cargo acceptance or rejection.
- Offline-first mobile operation and integrations with scanners, scales, printers, or other hardware.

These exclusions are not confirmed business decisions and should be reviewed during scope approval.

## 13. Open Business Questions

Answers are required before the affected requirements can be finalized.

### Service and scope

- Who may submit collection requests: external customers, internal teams, or both?
- Which regions, cargo types, and collection types are included in the MVP?
- Is collection on demand, appointment-based, time-window-based, or governed by another model?
- What are the business-defined conditions for completing a collection request?
- Are there service windows, cut-off times, capacity limits, or other commitments? If so, what exactly are they?

### Scheduling and collection outcomes

- Who may schedule, assign, cancel, or reschedule a collection, and at which workflow stages?
- What information and reason codes are required for a failed attempt?
- What follow-up options are valid after an unsuccessful collection?
- Can partial collections, repeated attempts, no-shows, refused access, or disputed handovers occur?

### Cargo and custody

- What is the precise business meaning of *collected*, *received*, *registered*, and *accepted*?
- Who may accept or refuse cargo, when is the decision made, and what evidence or reason is required?
- Can one request contain multiple cargo items? Can cargo be split or consolidated?
- Which cargo identifiers and attributes are required, and who issues identifiers?
- Which custody, location, handling, exception, and terminal events must be tracked?
- What handover evidence, if any, is required?

### Users and communications

- Are collection agents employees, contractors, or both? Do they require a mobile application?
- Which user groups may see customer details, cargo data, audit histories, and reports?
- Which events require notifications, to whom, through which channels, and with what delivery or retry expectations?
- Which queues and reports are essential for the first release?

### Quality, governance, and integrations

- What are expected usage and data volumes, response-time targets, availability expectations, and recovery objectives?
- Which audit records must be retained, who may view them, and for how long?
- What personal data is necessary, and what are the organization's retention and deletion rules?
- Which existing systems must integrate with the MVP, and which system is authoritative for each data type?
- What accessibility, browser, device, localization, and time-zone requirements apply?

## 14. Assumptions and Dependencies

The following are working assumptions or dependencies, not confirmed business rules:

- **A-001 (Proposed):** The MVP is intended to cover collection-request handling and cargo registration or operational tracking; final boundaries depend on stakeholder approval.
- **A-002 (Proposed):** Users will have distinct permissions based on approved responsibilities; the role model and identity approach remain **To Be Confirmed**.
- **A-003 (Proposed):** Request status and cargo status may represent different lifecycle decisions and should not be conflated.
- **A-004 (Proposed):** A collection attempt may fail; failure, cancellation, and rescheduling must be representable if they occur in the approved process.
- **A-005 (Proposed):** Cargo acceptance is an explicit business decision and is not implied by collection or registration.
- **D-001 (To Be Confirmed):** Business owners will define required request and cargo data, valid states and transitions, exception handling, and decision authority.
- **D-002 (To Be Confirmed):** Business and technical owners will define measurable security, performance, reliability, retention, and recovery criteria.
- **D-003 (To Be Confirmed):** Stakeholders will identify required external systems, authoritative data sources, and integration scope.
- **D-004 (To Be Confirmed):** The project/repository naming relationship between “MyFirstProfessionalApp” in the request and the current CargoTracking workspace will be clarified.

## 15. Approval Status

**Draft - Pending Business Review**

This document is a proposed initial MVP requirements analysis. Proposed requirements, user roles, workflows, acceptance criteria, exclusions, assumptions, and dependencies require review. Unresolved business questions must be answered or explicitly deferred by the appropriate stakeholders before the affected requirements are treated as approved or used as binding implementation scope.
