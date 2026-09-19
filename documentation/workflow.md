# Workflow Design

## End-to-End Flow

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

## Flow Designer Proposal

### Trigger

**When:** An Admission Request is submitted or moves to the Assessment state.

**Initial actions:** Validate required fields, set the request state, and notify the Registration Desk that the request was received.

### Stage 1: Doctor Assessment

1. Look up the assessment assignment group.
2. Create a Doctor Assessment task linked to the admission.
3. Assign the task to the selected doctor or Medical Assessment group.
4. Notify the assignee.
5. Wait until the task is completed, cancelled, or escalated.
6. If the assessment is incomplete, keep the admission open and notify the coordinator.

### Stage 2: Department Assignment

1. Read the selected or assessed department.
2. Map the department to an Assignment Group.
3. Update the admission with the department and group.
4. Create a Department Coordination task.
5. Use a fallback group and an exception notification when no mapping exists.

### Stage 3: Treatment and Investigation Tasks

Create child tasks based on the assessment and configured task types. Each task should contain the admission reference, task type, assignment group, owner, priority, due date, and status.

Use parallel branches where treatment and investigation work can happen independently. Use a join or condition that waits until all mandatory child tasks are complete. Optional tasks should not block discharge unless configured as mandatory.

### Stage 4: Discharge Readiness Check

When required tasks are complete:

1. Create or update the Discharge Request.
2. Check treatment status and investigation status.
3. Check required documentation and outstanding tasks.
4. Set Discharge Readiness to Ready or Not Ready.
5. If not ready, create a rework task and notify the coordinator.
6. If ready, continue to doctor approval.

### Stage 5: Doctor Approval

Use the Flow Designer Approval action to request approval from the assigned doctor. Include the admission number, patient reference, outstanding task summary, and readiness result.

- **Approved:** Set the request to Approved for Discharge and continue.
- **Rejected:** Capture the rejection reason, set the request to Rework Required, create a task for the responsible group, and notify the coordinator.
- **Cancelled or timed out:** Escalate according to the configured policy and keep the request open.

### Stage 6: Discharge Process and Summary

After approval, create a Discharge Coordination task. The coordinator confirms discharge details, completes the Discharge Summary, records follow-up requirements, and moves the admission to Discharged only after required fields are complete.

### Stage 7: Follow-up Activity

If Follow-up Required is true:

1. Create a Follow-up Activity with an appropriate due date.
2. Assign it to the selected follow-up group.
3. Send an approved discharge or follow-up notification.
4. Notify the responsible user before the due date.
5. Close the activity with an outcome and completion date.

## Flow Controls and Exceptions

- Use conditions to avoid duplicate child tasks when a flow is retried.
- Add error handling for missing assignment mappings and invalid references.
- Keep sensitive patient information out of broad group notifications.
- Use approvals for decisions, not for routine task completion.
- Log failure details for administrators without exposing them to patients.
