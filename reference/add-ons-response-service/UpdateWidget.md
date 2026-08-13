# UpdateWidget

A builder for `UpdateWidget` objects.

A builder for `UpdateWidget` objects. Developers can update a widget in the card by passing a `UpdateWidget` to `ModifyCard`. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### addSuggestion(text, value, selected, startIconUri, bottomText)

`addSuggestion(text: Object, value: Object, selected: Boolean, startIconUri: Object, bottomText: Object): UpdateWidget`

Adds a new item that can be selected, for multi-select menus.

**Parameters**
- `text` (Object) — The text to be shown for this item. Non-string primitive arguments are converted to strings automatically.
- `value` (Object) — The form input value that is sent via the callback. Non-string primitive arguments are converted to strings automatically.
- `selected` (Boolean) — Whether the item is selected by default. If the selection input only accepts one value (such as for radio buttons or a dropdown menu), only set this field for one item.
- `startIconUri` (Object) — For multiselect menus, the URL for the icon displayed next to the item's text field. Supports PNG and JPEG files.
- `bottomText` (Object) — For multiselect menus, a text description or label that's displayed below the item's text field.

**Returns**
- `UpdateWidget` — This update widget object, for chaining.
