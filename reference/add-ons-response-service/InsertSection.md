# InsertSection

A builder for InsertSection objects.

A builder for InsertSection objects. Developers can insert a new section to the card by passing a `InsertSection` to `ModifyCard`.

Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### insertAtTop(onCardTop)

`insertAtTop(onCardTop: Boolean): InsertSection`

Sets the onCardTop flag, which indicates whether the new section should be inserted at the top of the card.

**Parameters**
- `onCardTop` (Boolean) — The onCardTop flag.

**Returns**
- `InsertSection` — The insert section object, for chaining.

### insertBelowSection(sectionId)

`insertBelowSection(sectionId: String): InsertSection`

Sets the section ID, and the new section is inserted below it. If the section ID is not found, then the new section is inserted at the end of the card.

**Parameters**
- `sectionId` (String) — The ID of the section to insert below.

**Returns**
- `InsertSection` — The insert section object, for chaining.

### setSection(section)

`setSection(section: CardSection): InsertSection`

Sets the card section to be inserted.

**Parameters**
- `section` (CardSection) — The CardSection to be inserted.

**Returns**
- `InsertSection` — The insert section object, for chaining.

## Code Sample

```javascript
const insertSection = AddOnsResponseService.newInsertSection()
  .insertBelowSection('sample_id')
  .setSection(CardService.newCardSection().setHeader('New Section'));

const modifyCard = AddOnsResponseService.newModifyCard()
  .setInsertSection(insertSection);
```
