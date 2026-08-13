# WorkflowValidationErrorAction

Indicates that the host app should display a validation error.

This action indicates that the host app (Google Workspace Studio) should display a validation error. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setSeverity(severity)

`setSeverity(severity: ValidationErrorSeverity): WorkflowValidationErrorAction`

Sets the severity of the validation error.

**Parameters**
- `severity` (ValidationErrorSeverity) — The severity of the validation error.

**Returns**
- `WorkflowValidationErrorAction` — This workflow validation error action.

## Code Sample

```javascript
const hostAppAction = AddOnsResponseService.newHostAppAction()
   .setWorkflowAction(
     AddOnsResponseService.newWorkflowValidationErrorAction()
       .setSeverity(AddOnsResponseService.ValidationErrorSeverity.CRITICAL)
   );
```
