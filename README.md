# Hospital Patient Admission & Discharge Management System

## Project Overview

The **Hospital Patient Admission & Discharge Management System** is a ServiceNow application design for coordinating a patient's journey from registration through admission, treatment, discharge, and follow-up. It demonstrates how ServiceNow can connect clinical coordination tasks, departmental ownership, approvals, notifications, reporting, and knowledge articles in one controlled workflow.

This repository contains implementation documentation and test scenarios for a proposed project. It does not claim that the tables, flows, or configurations have already been created in a ServiceNow instance.

## Problem Statement

Hospitals often coordinate admissions, doctor assessments, investigations, treatment tasks, discharge approvals, and follow-up activities through disconnected channels. This can cause unclear ownership, missed tasks, delayed approvals, incomplete discharge records, and inconsistent communication with patients and staff.

## Project Objective

Design a traceable ServiceNow solution that:

- Captures patient and admission information in a structured record.
- Routes work to the right doctor, department, and assignment group.
- Tracks treatment and investigation tasks to completion.
- Validates discharge readiness before approval.
- Automates notifications and follow-up activities.
- Provides reporting and dashboard visibility for hospital operations.

## Business Scenario

A patient arrives at the hospital and is registered by front-desk staff. An admission request is created with the reason for admission and initial patient details. A doctor assesses the patient, and the system assigns the case to the appropriate department. Treatment and investigation tasks are created for department teams. When the required work is complete, the care team performs a discharge readiness check. The doctor approves or rejects discharge, after which staff complete the discharge process, record a discharge summary, and send follow-up instructions or tasks.

## System Workflow

```text
Patient Registration
  -> Admission Request
  -> Doctor Assessment
  -> Department Assignment
  -> Treatment/Investigation Tasks
  -> Discharge Readiness Check
  -> Doctor Approval
  -> Discharge Process
  -> Discharge Summary
  -> Follow-up Notification
```

## Key Features

- Patient registration and admission request tracking.
- Doctor assessment and clinical ownership.
- Department and assignment group routing.
- Treatment and investigation task management.
- Discharge readiness validation.
- Doctor approval with rejection and rework paths.
- Discharge summary capture.
- Patient and staff notifications.
- Reports and an operations dashboard.
- Knowledge articles for repeatable hospital procedures.

## ServiceNow Technologies Used

- Custom application and custom tables.
- Service Catalog and Catalog Items.
- Catalog Variables and variable sets.
- Flow Designer.
- Approval actions.
- Assignment Groups.
- Business Rules.
- Client Scripts.
- UI Policies.
- Notifications.
- Reports and dashboards.
- Knowledge Management.

## Custom Tables

The proposed data model is documented in [documentation/project-overview.md](documentation/project-overview.md). Core records include Patient, Admission Request, Treatment Task, Investigation Task, Discharge Request, and Follow-up Activity. Reference fields should connect operational records to users, departments, assignment groups, and the patient record rather than duplicating data.

### Suggested Patient Fields

- Patient ID
- Patient Name
- Age
- Contact Number
- Gender
- Department
- Assigned Doctor
- Admission Date
- Reason for Admission
- Room/Ward
- Treatment Status
- Investigation Status
- Discharge Readiness
- Follow-up Required

## Flow Designer Automation

A proposed admission flow can trigger when an Admission Request is submitted. It creates doctor assessment and department tasks, routes them to assignment groups, waits for treatment and investigation completion, checks discharge readiness, requests doctor approval, and then creates discharge and follow-up activities. The detailed flow logic and exception paths are in [documentation/workflow.md](documentation/workflow.md).

## Approval Process

The doctor approval step should only be requested after required treatment and investigation tasks are complete and the discharge readiness check passes. Approval can be approved, rejected with a reason, or sent back for rework. Rejection should create a follow-up task for the responsible team and keep the admission open.

## Notifications

Proposed notifications cover admission acknowledgement, new task assignment, overdue work, approval requests, approval rejection, discharge completion, and follow-up reminders. Notification recipients and message content should be configured according to hospital privacy and communication policies.

## Testing Scenarios

Test cases cover registration, routing, task completion, readiness validation, approval outcomes, notifications, and follow-up creation. Actual results are intentionally marked **Not Executed** because this repository does not include a ServiceNow instance. See [documentation/testing.md](documentation/testing.md).

## Screenshots

No screenshots are included yet. [screenshots/README.md](screenshots/README.md) contains placeholders and a capture checklist for screenshots taken after implementation in a ServiceNow Developer Instance.

## Future Enhancements

- Patient portal or employee self-service intake.
- Integration with hospital information systems through IntegrationHub or REST APIs.
- Role-based access with stronger clinical data controls.
- SLA timers and escalation for critical tasks.
- Bed and ward availability integration.
- SMS or approved external communication provider integration.
- ServiceNow Performance Analytics for wait-time and discharge trends.
- Mobile-friendly task execution for clinical staff.

## Skills Demonstrated

- ServiceNow application and data model design.
- Service Catalog configuration.
- Flow Designer orchestration.
- Approval and assignment design.
- Business Rules, Client Scripts, and UI Policies.
- Notifications, reports, dashboards, and knowledge design.
- Requirements analysis and workflow documentation.
- Test case design and implementation readiness.

## Repository Guide

- [Project Overview](documentation/project-overview.md)
- [Implementation Guide](documentation/implementation.md)
- [Workflow Design](documentation/workflow.md)
- [Testing Plan](documentation/testing.md)
- [Screenshot Placeholders](screenshots/README.md)
- [Update Set Notes](update-set/README.md)
