# Project Overview

## Purpose

This document defines the proposed ServiceNow solution for coordinating hospital patient admission and discharge activities. It is a design and implementation reference for a B.Tech CSE fresher portfolio project.

## Scope

### In Scope

- Patient registration and admission requests.
- Doctor assessment and department assignment.
- Treatment and investigation task tracking.
- Discharge readiness and doctor approval.
- Discharge summary and follow-up activity.
- Notifications, reporting, dashboard visibility, and knowledge guidance.

### Out of Scope

- Real patient data or production clinical decisions.
- Medical diagnosis or treatment recommendations.
- Billing, insurance, pharmacy, and laboratory system integrations.
- HIPAA or other regulatory certification.

## Proposed Application Roles

| Role | Responsibility |
|---|---|
| Registration Clerk | Creates patient and admission records. |
| Doctor | Performs assessment, reviews readiness, and approves or rejects discharge. |
| Department Coordinator | Assigns and monitors departmental work. |
| Nurse or Care Coordinator | Updates treatment, investigation, and readiness information. |
| Discharge Coordinator | Completes discharge processing and summary. |
| Application Administrator | Maintains configuration, flows, security, and reporting. |

## Proposed Custom Tables

| Table | Purpose | Key fields |
|---|---|---|
| Patient | Stores the patient profile used by related records. | Patient ID, name, age, contact, gender |
| Admission Request | Tracks the patient's admission journey. | Patient, admission date, reason, department, doctor, ward, state |
| Treatment Task | Tracks treatment work assigned to a department. | Admission, task type, owner, status, due date |
| Investigation Task | Tracks diagnostic or investigation work. | Admission, investigation type, owner, status, result reference |
| Discharge Request | Controls readiness and approval for discharge. | Admission, readiness, doctor approval, rejection reason |
| Follow-up Activity | Tracks post-discharge communication and work. | Patient, admission, activity type, due date, status |

Use reference fields for users, groups, departments, patients, and admissions wherever possible. Add audit fields and choice values for state, priority, status, and readiness.

## Patient Data Fields

The Patient table should support the following requested fields: Patient ID, Patient Name, Age, Contact Number, Gender, Department, Assigned Doctor, Admission Date, Reason for Admission, Room/Ward, Treatment Status, Investigation Status, Discharge Readiness, and Follow-up Required.

For maintainability, fields that describe a specific admission, such as Room/Ward and Treatment Status, may be stored on Admission Request while the Patient table stores stable identity and contact information. This separation avoids overwriting historical admission details.

## Success Measures

- Every admission has a visible owner and current state.
- Departmental work can be traced to an admission.
- Discharge cannot be approved while required work is incomplete.
- Staff receive actionable notifications at key transitions.
- Managers can report on open admissions, delays, and follow-ups.
