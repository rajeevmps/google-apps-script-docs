# Drive Manifest Resource Documentation

## Drive

The Google Workspace add-on manifest configuration for Google Drive extensions. See [Extending Drive with Google Workspace add-ons](https://developers.google.com/workspace/add-ons/drive) for more information.

**JSON representation**

```json
{
  "homepageTrigger": {
    object (HomepageTrigger)
  },
  "onItemsSelectedTrigger": {
    object (OnItemsSelectedTrigger)
  }
}
```

**Fields**

| Field | Type | Description |
|-------|------|-------------|
| `homepageTrigger` | object (HomepageTrigger) | The trigger function for the add-on [homepage](https://developers.google.com/workspace/add-ons/concepts/homepages) in the Drive host. This overrides `addOns.common.homepageTrigger`. |
| `onItemsSelectedTrigger` | object (OnItemsSelectedTrigger) | **Required to provide add-on behavior triggered by user selection of items in Drive**. The contextual trigger function for item selections in Google Drive. |

## OnItemsSelectedTrigger

A configuration for a contextual trigger that fires when a user selects files or folders in Google Drive. See [Drive contextual interface for items selected](https://developers.google.com/workspace/add-ons/drive/building-drive-interfaces#drive_contextual_interface_for_items_selected) for details.

**JSON representation**

```json
{
  "runFunction": string
}
```

**Fields**

| Field | Type | Description |
|-------|------|-------------|
| `runFunction` | string | The name of the function to run when files or folders are selected in Google Drive. The function must return an array of [`Card`](https://developers.google.com/apps-script/reference/card-service/card) objects for the UI. |

Source: https://developers.google.com/apps-script/manifest/drive-addons
