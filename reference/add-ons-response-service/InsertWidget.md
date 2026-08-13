# InsertWidget

A builder for InsertWidget objects.

A builder for InsertWidget objects. Developers can insert a widget into a card by passing a `InsertWidget` to `ModifyCard`.

Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### insertAboveWidget(widgetId)

`insertAboveWidget(widgetId: String): InsertWidget`

Sets the widget ID, and the new widget is inserted above the widget with the given ID. An error is thrown if the widget ID is not found.

**Parameters**
- `widgetId` (String) — The ID of the widget to insert above.

**Returns**
- `InsertWidget` — The insert widget object, for chaining.

### insertBelowWidget(widgetId)

`insertBelowWidget(widgetId: String): InsertWidget`

Sets the widget ID, and the new widget is inserted below the widget with the given ID. An error is thrown if the widget ID is not found.

**Parameters**
- `widgetId` (String) — The ID of the widget to insert below.

**Returns**
- `InsertWidget` — The insert widget object, for chaining.

### setWidget(widget)

`setWidget(widget: Widget): InsertWidget`

Sets the `Widget` to be inserted. An error is thrown if there is a existing widget with the same ID.

**Parameters**
- `widget` (Widget) — The widget to be inserted.

**Returns**
- `InsertWidget` — The insert widget object, for chaining.

## Code Sample

```javascript
const newWidget = CardService.newDecoratedText().setText('New Widget');
const insertWidget = AddOnsResponseService.newInsertWidget()
                                          .insertAboveWidget('sample_id')
                                          .setWidget(newWidget);
const modifyCard = AddOnsResponseService.newModifyCard().setInsertWidget(insertWidget);
```
