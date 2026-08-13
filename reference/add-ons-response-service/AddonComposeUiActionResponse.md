# AddonComposeUiActionResponse

Represents an action on the addon compose ui.

Represents an action on the addon compose ui.

## Methods

### printJson()

`printJson(): String`

Prints the JSON representation of this object. This is for debugging only.

## Code Sample

```javascript
const addonComposeUiActionResponse =
    AddOnsResponseService.newAddonComposeUiActionResponseBuilder()
        .setType(AddOnsResponseService.AddonComposeUiActionType.DISMISS)
        .build();
```

This example demonstrates creating an AddonComposeUiActionResponse that dismisses the addon compose UI.
