# Action

An action that Google Workspace add-ons that extend Google Workspace Studio can use to render a new card.

An action that Google Workspace add-ons that extend Google Workspace Studio can use to render a new card. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### addModifyCard(modifyCard)

`addModifyCard(modifyCard: ModifyCard): Action`

Adds a ModifyCard operation to the action.

**Parameters**
- `modifyCard` (ModifyCard) — The ModifyCard to use.

**Returns**
- `Action` — This action object, for chaining.

### addNavigation(navigation)

`addNavigation(navigation: Navigation): Action`

Adds a card navigation to the action.

**Parameters**
- `navigation` (Navigation) — The Navigation to use.

**Returns**
- `Action` — This action object, for chaining.

**Throws:** Error if the navigation argument is invalid.

## Code Sample

```javascript
const link = AddOnsResponseService.newLink().setUrl('https://www.google.com');
const action =
    AddOnsResponseService.newAction()
        .setLink(link);

const renderAction = AddOnsResponseService.newRenderActionBuilder()
    .setAction(action).build();
```
