# Build Google Drive interfaces

Google Workspace add-ons can provide customized interfaces when a user opens Drive. This lets you provide the user with additional relevant information, automate tasks, and connect third-party systems to Drive.

## Access the Google Workspace add-on UI

You can open add-on in Drive if its icon appears in the icon column on the right side of the Drive user interface. An add-on can define a homepage interface, an item select interface, or both:

- If a user clicks the add-on icon while in Drive, the add-on executes the corresponding `drive.homepageTrigger` function (if present). This function builds and returns a homepage card to Drive for display. If no `drive.homepageTrigger` function is defined, a generic homepage card is displayed instead.
- If the user selects one or more items in Drive and then clicks the add-on icon, or selects items while the add-on is open, the add-on executes the corresponding `drive.onItemsSelectedTrigger` contextual function (if present). This function builds the add-on's Drive contextual "items selected" interface and returns it to Drive for display.

## Build the add-on Drive interface

Build interfaces that extend Drive by following these general steps:

1. Decide whether you want your add-on to have a Drive-specific homepage. Also decide if you want to provide a contextual interface for when the user selects Drive items.
2. Add the appropriate `addOns.common` and `addOns.drive` fields to the add-on script project manifest, including any Drive scopes required.
3. If you are providing a Drive-specific homepage, implement the `drive.homepageTrigger` function to build this interface. You can also choose to use the `common.homepageTrigger` interface for multiple Google Workspace hosts.
4. If you are providing a Drive contextual item selection interface, you must implement a `drive.onItemsSelectedTrigger` contextual trigger function to build this interface. See Drive contextual interface for items selected for details.
5. Implement the associated callback functions needed to respond to the user's UI interactions, such as button clicks.

## Drive homepages

Drive supports displaying add-on homepages. To show your add-on's common homepage in Drive ensure there is a `addOns.drive` field in the add-on's manifest.

Alternatively, add a `drive.homepageTrigger` to the add-on manifest to provide a Drive-specific homepage.

In either case, provide the name of a homepage trigger function in your add-on's script project. This function is automatically called to build the Drive homepage when it is needed. Implement this function to build and return a single Card or an array of Card objects that make up the homepage. The homepage trigger function is passed an event object as a parameter that contains some general information such as the client's platform. Use the event object data to build the homepage.

## Drive contextual interface for items selected

Drive relies on a contextual trigger to determine what interface (if any) to display when the user selects one or more Drive items. When the trigger fires, it executes the contextual trigger function specified by the `drive.onItemsSelectedTrigger.runFunction` field in the add-on manifest.

To create a contextual item selection interface for Drive, you must do the following:

1. Ensure the add-on's manifest includes the `https://www.googleapis.com/auth/drive.addons.metadata.readonly` scope.
2. Ensure the manifest includes a `drive.onItemsSelectedTrigger` section.
3. Implement the function named in the `drive.onItemsSelectedTrigger` field. This function accepts an event object as an argument and must return either a single Card object or an array of Card objects.
4. As with any card, implement any callback functions used to provide widget interactivity for the interface. For example, if you include a button in the interface, it should have an attached Action and an implemented callback function that run when the button is clicked.

## Event objects

An event object is created and passed to the `drive.homepageTrigger` or `drive.onItemsSelectedTrigger` trigger function when those functions are called. The trigger function uses the information in this event object to determine how to build add-on cards or otherwise control the add-on behavior.

The full structure of event objects is described in Event objects. When Drive is the acting host app of the add-on, contextual event objects include the Drive event object field that carries Drive-specific client information.

Contextual Drive event objects for item selection triggers include information about the items the user has selected when the trigger fires. When a user selects more than one item in Drive, one of the items is deemed to be one of primary interest; this item is referred to as the active cursor item.

If the add-on's behavior is meant to apply to multiple selected items, use the information provided in the `drive.selectedItems` array in the event object to identify them all.

When an add-on's behavior should only be applied to a single selected item, use the information provided in the `drive.activeCursorItem` field of the event object to identify the item out of the full selection. Don't attempt to infer which item to use from the `drive.selectedItems` array.

The following example shows a Drive event object that is passed to a `drive.onItemsSelectedTrigger` function:

```json
{
  "commonEventObject": { ... },
  "drive": {
    "activeCursorItem":{
      "addonHasFileScopePermission": true,
      "id":"0B_sX1fXRRU6Ac3RhcnRlcl9maWxl",
      "iconUrl": "https://drive-thirdparty.googleusercontent.com...",
      "mimeType":"application/pdf",
      "title":"How to get started with Drive"
    },
    "selectedItems": [
      {
        "addonHasFileScopePermission": true,
        "id":"0B_sX1fXRRU6Ac3RhcnRlcl9maWxl",
        "iconUrl":"https://drive-thirdparty.googleusercontent.com...",
        "mimeType":"application/pdf",
        "title":"How to get started with Drive"
      },
      ...
    ]
  },
  ...
}
```
