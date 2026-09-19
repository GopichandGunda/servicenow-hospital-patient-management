# Testing Plan

## Test Data and Execution Notes

Use synthetic patient data only. Execute these cases in a configured ServiceNow Developer Instance after tables, catalog items, flows, roles, notifications, and reports are implemented. The Actual Result and Status columns are intentionally marked **Not Executed** in this repository.

## Test Cases

| Test Case ID | Scenario | Input | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|
| TC-001 | Submit a complete admission request | Valid patient identity, contact, reason, department, and follow-up value | Admission Request is created with a number, initial state, and acknowledgement notification | Not Executed | Not Executed |
| TC-002 | Reject an incomplete admission request | Omit required Reason for Admission | Catalog validation prevents submission and identifies the missing field | Not Executed | Not Executed |
| TC-003 | Route doctor assessment | Submitted admission with a mapped department and assigned doctor | Doctor Assessment task is created and assigned to the doctor or Medical Assessment group | Not Executed | Not Executed |
| TC-004 | Handle missing department mapping | Admission uses a department without an Assignment Group mapping | Flow uses the fallback group and sends an exception notification | Not Executed | Not Executed |
| TC-005 | Create parallel care tasks | Assessment requires treatment and investigation work | Treatment Task and Investigation Task records are created with the correct references and groups | Not Executed | Not Executed |
| TC-006 | Block readiness with open mandatory work | One mandatory investigation task remains open | Discharge Readiness is Not Ready and doctor approval is not requested | Not Executed | Not Executed |
| TC-007 | Request approval after readiness | All mandatory treatment and investigation tasks are complete | Discharge Request is created or updated and approval is sent to the assigned doctor | Not Executed | Not Executed |
| TC-008 | Approve discharge | Doctor selects Approve | Admission advances to discharge processing and a discharge task is created | Not Executed | Not Executed |
| TC-009 | Reject discharge approval | Doctor selects Reject and enters a reason | Rejection is recorded, rework task is created, and coordinator is notified | Not Executed | Not Executed |
| TC-010 | Prevent incomplete discharge closure | Coordinator attempts closure without a discharge summary | UI or server-side validation prevents closure and identifies required fields | Not Executed | Not Executed |
| TC-011 | Complete discharge with follow-up | Approval is granted, summary is complete, Follow-up Required is true | Admission is discharged, follow-up activity is created, and notification is sent | Not Executed | Not Executed |
| TC-012 | Complete discharge without follow-up | Approval is granted, summary is complete, Follow-up Required is false | Admission is discharged and no follow-up activity is created | Not Executed | Not Executed |
| TC-013 | Verify overdue task notification | Assigned task passes its due date | Configured reminder or escalation notification is sent to the owner or group | Not Executed | Not Executed |
| TC-014 | Verify dashboard reporting | Create records across departments and states | Reports show correct counts and dashboard filters return matching records | Not Executed | Not Executed |
| TC-015 | Verify role access | User signs in with registration, doctor, coordinator, and admin roles | Each role can access only its permitted records and actions | Not Executed | Not Executed |

## Exit Criteria

- All critical and high-priority cases pass.
- No admission can bypass required readiness and approval controls.
- Notifications are received by intended recipients without prohibited sensitive data.
- Reports reconcile with the underlying test records.
- Any failed case has a documented defect and retest result.
