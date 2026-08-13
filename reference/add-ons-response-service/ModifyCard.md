# ModifyCard

A builder for `ModifyCard` objects that changes and updates an existing card's interface.

A builder for `ModifyCard` objects that changes and updates an existing card's interface by passing the `ModifyCard` object to a `Action`. For usage, see Update configuration cards.

Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setInsertSection(insertSection)

`setInsertSection(insertSection: InsertSection): ModifyCard`

Sets the `InsertSection` for this modify card object.

### setInsertWidget(insertWidget)

`setInsertWidget(insertWidget: InsertWidget): ModifyCard`

Sets the `InsertWidget` for this modify card object.

### setRemoveSection(removeSection)

`setRemoveSection(removeSection: RemoveSection): ModifyCard`

Sets the `RemoveSection` for this modify card object.

### setRemoveWidget(removeWidget)

`setRemoveWidget(removeWidget: RemoveWidget): ModifyCard`

Sets the `RemoveWidget` for this modify card object.

### setReplaceSection(replacementSection)

`setReplaceSection(replacementSection: CardSection): ModifyCard`

Sets the replacement `CardSection` for this modify card object, the replacement section should have the same id as an existing card section.

### setReplaceWidget(replacementWidget)

`setReplaceWidget(replacementWidget: Widget): ModifyCard`

Sets the replacement widget for this modify card object, the replacement widget should have the same id as an existing widget.

### setUpdateWidget(updateWidget)

`setUpdateWidget(updateWidget: UpdateWidget): ModifyCard`

Sets the `UpdateWidget` for this modify card object.

## Code Sample

```javascript
const insertSection = AddOnsResponseService.newInsertSection().insertBelowSection('sample_id')
.setSection(CardService.newCardSection().setHeader('New Section'));

const modifyCard = AddOnsResponseService.newModifyCard().setInsertSection(insertSection);

const navigation = AddOnsResponseService.newNavigation().addModifyCard(modifyCard);
```
