# Update Set Notes

This folder is reserved for update-set documentation and exported artifacts after configuration in a ServiceNow Developer Instance.

## Proposed Packaging Units

1. **01 - Data Model**: custom tables, fields, choices, relationships, and number definitions.
2. **02 - Service Catalog**: catalog item, catalog variables, variable sets, and producer configuration.
3. **03 - Security and Routing**: roles, ACLs, assignment groups, and department mappings.
4. **04 - Automation**: Flow Designer flows, subflows, approval actions, and error handling.
5. **05 - Form Experience**: Client Scripts, UI Policies, form layouts, and related lists.
6. **06 - Communication**: notifications, email templates, and events.
7. **07 - Reporting and Knowledge**: reports, dashboard, and knowledge articles.

## Promotion Checklist

- Use a meaningful update-set name and description.
- Keep configuration changes grouped by logical feature.
- Preview the update set in the target instance.
- Resolve collisions and review skipped records.
- Test in the target instance with synthetic data.
- Export or commit only artifacts that are safe to share.
- Record the ServiceNow release, scope, test date, and deployment notes.

No update-set XML or claim of completed configuration is included in this repository at present.
