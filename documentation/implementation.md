# Implementation Guide

This guide describes a proposed implementation sequence. Configuration must be performed and verified in a ServiceNow Developer Instance before it can be represented as completed.

## 1. Application and Data Model

1. Create a scoped application for hospital patient management.
2. Create the Patient, Admission Request, Treatment Task, Investigation Task, Discharge Request, and Follow-up Activity tables.
3. Add labels, help text, choice values, reference fields, audit fields, and number formats.
4. Define relationships so an admission can have multiple treatment, investigation, and follow-up records.
5. Apply roles and access controls appropriate for front-desk, clinical, coordinator, and administrator users.

## 2. Service Catalog

Create a catalog item named **Request Patient Admission** for registration staff or an approved requester. The item should create an Admission Request and capture the minimum information needed for assessment.

### Catalog Variables

| Variable | Type | Required | Purpose |
|---|---|---:|---|
| Patient ID | Single line text | Yes | Identifies an existing patient or supports a lookup process. |
| Patient Name | Single line text | Yes | Displays the patient name for the request. |
| Age | Integer | Yes | Captures age at admission. |
| Contact Number | Single line text | Yes | Enables approved communication. |
| Gender | Choice | Yes | Captures the selected value. |
| Reason for Admission | Multi-line text | Yes | Records the presenting reason. |
| Preferred Department | Reference or choice | Yes | Supports initial routing. |
| Room/Ward | Reference or choice | No | Captures the known placement. |
| Follow-up Required | Yes/No | Yes | Indicates whether follow-up should be planned. |

Use a variable set for reusable patient identity fields if the catalog grows. Validate sensitive data handling and do not use real patient information in development.

## 3. Automation Components

### Flow Designer

Create an admission flow with a trigger on a submitted Admission Request. Use actions and subflows to create tasks, assign groups, wait for completion, evaluate conditions, request approval, and create follow-up activities.

### Business Rules

Proposed rules include:

- Set the initial admission state and number.
- Prevent a discharge request from closing when required work is incomplete.
- Stamp completion dates when tasks transition to complete.
- Create an audit entry when approval is rejected.

Business Rules should enforce server-side data integrity. They should not duplicate Flow Designer work unless there is a clear transaction requirement.

### Client Scripts

Use Client Scripts for form behavior such as setting a default department, validating a contact number format, or showing a rejection reason when the approval state is rejected. Critical validation must also exist server-side.

### UI Policies

Use UI Policies to make fields mandatory, visible, or read-only by state. For example, make Rejection Reason mandatory when Doctor Approval is Rejected and make discharge fields read-only after final closure.

## 4. Assignment Groups

Create or map groups such as Registration Desk, Medical Assessment, Nursing, Diagnostics, Pharmacy or Treatment Coordination, Discharge Coordination, and Hospital Application Support. Group selection should be driven by department and task type, with a fallback group for routing exceptions.

## 5. Notifications

Configure event- or condition-based notifications for admission acknowledgement, new assignment, overdue work, doctor approval request, rejection with rework instructions, discharge completion, and follow-up reminders. Use templates with record numbers and approved non-sensitive details.

## 6. Reports and Dashboard

Suggested reports include open admissions by state, average time from request to assessment, incomplete tasks by department, pending doctor approvals, discharge delays, and follow-ups due. Combine these reports into an operations dashboard with filters for department, date, priority, and state.

## 7. Knowledge Management

Create draft knowledge articles for admission registration, department routing, discharge readiness criteria, approval handling, and follow-up procedures. Set ownership, review dates, audience, and approval workflow before publishing.

## 8. Delivery and Governance

Build in a development scope, test with non-production data, document configuration decisions, capture update sets by logical change, and promote only after peer review and test evidence are complete. The separate [update-set/README.md](../update-set/README.md) records the intended packaging approach.
