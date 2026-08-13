# ChatSpaceDataSource

A data source that populates Google Chat spaces as selection items for a multiselect menu.

A data source that populates Google Chat spaces as selection items for a multiselect menu. Only populates spaces that the user is a member of.

This class is exclusively available for Google Chat apps and not for Google Workspace add-ons.

```javascript
const chatSpaceDataSource =
    CardService.newChatSpaceDataSource().setDefaultToCurrentSpace(true);
```

## Methods

### setDefaultToCurrentSpace(defaultToCurrentSpace: Boolean): ChatSpaceDataSource

If set to `true`, the multi select menu selects the current Google Chat space as an item by default.

Parameters: `defaultToCurrentSpace` (Boolean) — The boolean to be set.

Returns: This object, for chaining.
