# HostAppAction

A type of Action that is handled by individual host apps.

A HostAppAction is a type of Action that is handled by individual host apps. Host Apps include Gmail, Chat, Drive, Calendar, Editor, Sheets, Studio, DuetAI. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setWorkflowAction(workflowAction)

`setWorkflowAction(workflowAction: WorkflowAction): HostAppAction`

Sets the host app action to Workflow action.

**Parameters**
- `workflowAction` (WorkflowAction) — The Workflow action.

**Returns**
- `HostAppAction` — This object, for chaining.

## Code Sample

```javascript
const hostAppAction = AddOnsResponseService.newHostAppAction()
  .setWorkflowAction(AddOnsResponseService.newWorkflowAction());
```
