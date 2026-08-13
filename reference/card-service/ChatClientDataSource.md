# ChatClientDataSource

A data source for a multiselect menu in a SelectionInput widget, specifically for Google Chat.

ChatClientDataSource is a data source for a multiselect menu in a SelectionInput widget, specifically for Google Chat. It populates selection items, for example, Google Chat spaces the user is a member of. This feature is exclusively available for Google Chat apps and not for Google Workspace add-ons.

```javascript
const chatSpaceDataSource =
    CardService.newChatSpaceDataSource().setDefaultToCurrentSpace(true);

const chatClientDataSource =
    CardService.newChatClientDataSource().setSpaceDataSource(
        chatSpaceDataSource);
```

## Methods

### setSpaceDataSource(spaceDataSource: ChatSpaceDataSource): ChatClientDataSource

A data source that populates Google Chat spaces as selection items for a multiselect menu. Only populates spaces that the user is a member of.

Parameters: `spaceDataSource` (ChatSpaceDataSource) — The data source to be set.

Returns: `ChatClientDataSource` — This object, for chaining.

Only available for Google Chat apps. Not available for Google Workspace add-ons.
