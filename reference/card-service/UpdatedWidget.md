# UpdatedWidget

The response of the updated widget.

The response of the updated widget. Used to provide autocomplete options for multiselect menu in `SelectionInput`.

UpdatedWidget is used to provide autocomplete options for multiselect menus in SelectionInput. It is only available for Google Chat apps and not Google Workspace add-ons.

```javascript
const updatedWidget = CardService.newUpdatedWidget()
    .addItem(
        'item_one_title',
        'item_one_value',
        false,
        'item_one_uri',
        'item_one_bottom_text',
    )
    .addItem(
        'item_two_title',
        'item_two_value',
        false,
        'item_two_uri',
        'item_two_bottom_text',
    );
```

## Methods

### addItem(text: Object, value: Object, selected: Boolean, startIconUri: Object, bottomText: Object): UpdatedWidget

Adds a new item that can be selected.

Parameters:
- `text` (Object): The text to be shown for this item. Non-string primitive arguments are converted to strings automatically.
- `value` (Object): The form input value that is sent via the callback. Non-string primitive arguments are converted to strings automatically.
- `selected` (Boolean): Whether the item is selected by default. If the selection input only accepts one value (such as for radio buttons or a dropdown menu), only set this field for one item.
- `startIconUri` (Object): For multiselect menus, the URL for the icon displayed next to the item's text field. Supports PNG and JPEG files.
- `bottomText` (Object): For multiselect menus, a text description or label that's displayed below the item's text field.

Returns: This object, for chaining.
