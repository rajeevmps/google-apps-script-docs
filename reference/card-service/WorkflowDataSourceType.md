# WorkflowDataSourceType

An enum that represents the type of the workflow data source.

An enum that represents the type of the workflow data source. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Properties

### UNKNOWN
Default value. Don't use.

### USER
The data source is a user's data.

### SPACE
The data source is a Google Chat space.

### USER_WITH_FREE_FORM
The data source is a user's data; users can choose to view and select existing members from their Google Workspace organization or manually enter an email address or a valid domain.

## Code Sample

```javascript
const workflowDataSource = CardService.newWorkflowDataSource().setIncludeVariables(true)
.setType(CardService.WorkflowDataSourceType.USER);
```
