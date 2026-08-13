# ReturnElementErrorAction

Indicates that an error occurred during element invocation.

A ReturnElementErrorAction indicates that an error occurred during element invocation. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setErrorActionability(errorActionability)

`setErrorActionability(errorActionability: ErrorActionability): ReturnElementErrorAction`

Sets the error actionability, an error should be actionable if it can be resolved by re-configuring the step. A "Fix it" link is displayed to the user to re-configure the step.

### setErrorLog(log)

`setErrorLog(log: WorkflowTextFormat): ReturnElementErrorAction`

Sets the error log to be displayed to the end user at Workflow's activity feed.

### setErrorRetryability(errorRetryability)

`setErrorRetryability(errorRetryability: ErrorRetryability): ReturnElementErrorAction`

Sets the error retry-ability, the flow terminates after the first try if an error is not retryable. Otherwise, Workflow is going to try to execute the Step for up to 5 times.

## Code Sample

```javascript
const workflowAction = AddOnsResponseService.newReturnElementErrorAction()
.setErrorActionability(
  AddOnsResponseService.ErrorActionability.NOT_ACTIONABLE
)
.setErrorRetryability(
  AddOnsResponseService.ErrorRetryability.NOT_RETRYABLE
)
.setErrorLog(
  AddOnsResponseService.newWorkflowTextFormat()
    .addTextFormatElement(
      AddOnsResponseService.newTextFormatElement()
        .setText("Failed to create Google Doc.")
    )
);
```
