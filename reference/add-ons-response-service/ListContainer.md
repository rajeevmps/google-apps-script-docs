# ListContainer

Container for list items, where each list item can contain multiple `TextFormatElement`.

Container for list items, where each list item can contain multiple `TextFormatElement`. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### addListItem(listItem)

`addListItem(listItem: ListItem): ListContainer`

Adds a list item to the list container.

**Parameters**
- `listItem` (ListItem) — The ListItem to be added to the list container.

### setListNestLevel(listLevel)

`setListNestLevel(listLevel: Integer): ListContainer`

Sets the level of the list, starts from 0 for the top level, and increases by 1 for each nested list.

**Parameters**
- `listLevel` (Integer) — The number of nest levels of the list.

### setListType(listType)

`setListType(listType: ListType): ListContainer`

Sets the type of the list to be ordered or unordered.

**Parameters**
- `listType` (ListType) — The ListType of the list.

## Code Sample

```javascript
const listContainer = AddOnsResponseService.newListContainer()
      .setListType(AddOnsResponseService.ListType.UNORDERED)
      .addListItem(
        AddOnsResponseService.newListItem()
          .addTextFormatElement(
            AddOnsResponseService.newTextFormatElement()
              .setStyledText(sampleStyledText)
          ));
```
