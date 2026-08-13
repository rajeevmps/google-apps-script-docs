# HostAppDataSource

For a `SelectionInput` widget that uses a multiselect menu, a data source from a Google Workspace application. The data source populates selection items for the multiselect menu.

HostAppDataSource is used with SelectionInput widgets in multiselect menus to populate items from a Google Workspace application data source. Only available for Google Chat apps and Google Workspace add-ons that extend flows.

## Methods

### setChatDataSource(chatClientDataSource: ChatClientDataSource): HostAppDataSource

Sets the data source from Google Chat. Only available for Google Chat apps. Not available for Google Workspace add-ons.

Parameters:
- `chatClientDataSource` (ChatClientDataSource) - The data source to be set.

Returns: This object, for chaining.

```javascript
const chatSpaceDataSource =
    CardService.newChatSpaceDataSource().setDefaultToCurrentSpace(true);

const chatClientDataSource =
    CardService.newChatClientDataSource().setSpaceDataSource(
        chatSpaceDataSource);

const hostAppDataSource =
    CardService.newHostAppDataSource().setChatDataSource(chatClientDataSource);
```

### setWorkflowDataSource(workflowDataSource: WorkflowDataSource): HostAppDataSource

Sets the data source from Google Workspace Flows. Only available for Google Workspace add-ons that extend Google Workspace Studio.

Parameters:
- `workflowDataSource` (WorkflowDataSource) - The data source to be set.

Returns: This object, for chaining.

```javascript
const workflowDataSource =
    CardService.newWorkflowDataSource().setIncludeVariables(true);

const hostAppDataSource =
    CardService.newHostAppDataSource().setWorkflowDataSource(workflowDataSource);
```
