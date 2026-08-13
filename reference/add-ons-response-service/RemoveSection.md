# RemoveSection

A builder for `RemoveSection` objects.

A builder for `RemoveSection` objects. Developers can remove a section from the card by passing a `RemoveSection` to `ModifyCard`.

Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setSectionId(sectionId)

`setSectionId(sectionId: String): RemoveSection`

Sets the section ID of the section to be removed.

**Parameters**
- `sectionId` (String) — The ID of the section to be removed.

**Returns**
- `RemoveSection` — This remove section object, for chaining.

## Code Sample

```javascript
const removeSection = AddOnsResponseService.newRemoveSection()
  .setSectionId('sample_id');

const modifyCard = AddOnsResponseService.newModifyCard()
  .setRemoveSection(removeSection);
```
