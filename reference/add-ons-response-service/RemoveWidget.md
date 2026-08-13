# RemoveWidget

A builder for RemoveWidget objects.

A builder for RemoveWidget objects. Developers can remove a widget from the card by passing a `RemoveWidget` to `ModifyCard`.

Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setWidgetId(widgetId)

`setWidgetId(widgetId: String): RemoveWidget`

Sets the widget ID of the widget to be removed.

**Parameters**
- `widgetId` (String) — The ID of the widget to remove.

**Returns**
- `RemoveWidget` — The remove widget object.

## Code Sample

```javascript
const removeWidget = AddOnsResponseService.newRemoveWidget()
  .setWidgetId('sample_id');

const modifyCard = AddOnsResponseService.newModifyCard()
  .setRemoveWidget(removeWidget);
```
