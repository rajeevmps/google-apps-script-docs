# WorkflowAction

A type of `HostAppAction` used to perform a specific action in Google Workspace Studio.

A WorkflowAction is a type of `HostAppAction` that is used to perform a specific action in Google Workspace Studio.

The class can represent one of these action types:
- `SaveWorkflowAction`
- `ReturnOutputVariablesAction`
- `ReturnElementErrorAction`
- `ResourceRetrievedAction`
- `WorkflowValidationErrorAction`
- `ResourceFieldsDefinitionRetrievedAction`

Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

The reference page does not include detailed method signatures, property listings, or return types for the WorkflowAction class itself beyond its role description and the related action classes listed above.

## Code Sample

```javascript
const hostAppAction = AddOnsResponseService.newHostAppAction();
hostAppAction.setWorkflowAction(AddOnsResponseService.newSaveWorkflowAction());
```
