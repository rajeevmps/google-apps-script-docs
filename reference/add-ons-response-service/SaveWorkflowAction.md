# SaveWorkflowAction

Indicates that the host app should save the agent.

This action indicates that the host app (Google Workspace Studio) should save the agent. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

No specific methods are documented for the `SaveWorkflowAction` class on the reference page beyond the description above.

## Code Sample

```javascript
const workflowClientAction = AddOnsResponseService.newWorkflowClientAction()
    .setSaveWorkflowAction(
       AddOnsResponseService.newSaveWorkflowAction()
    );
```
