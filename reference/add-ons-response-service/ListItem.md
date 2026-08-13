# ListItem

A list item, where each list item can contain multiple `TextFormatElement`.

A list item, where each list item can contain multiple `TextFormatElement`. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### addTextFormatElement(textFormatElement)

`addTextFormatElement(textFormatElement: TextFormatElement): ListItem`

Adds a `TextFormatElement` to the list item.

**Parameters**
- `textFormatElement` (TextFormatElement) — The `TextFormatElement` to add to the list item.

**Returns**
- `ListItem` — This list item object, for chaining.

## Code Sample

```javascript
const listItem = AddOnsResponseService.newListItem()
      .addTextFormatElements(AddOnsResponseService.newStyledText());
```
