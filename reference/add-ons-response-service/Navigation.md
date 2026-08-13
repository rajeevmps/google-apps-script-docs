# Navigation

A helper object that controls card navigation.

A helper object that controls card navigation. See the card navigation guide for more details.

## Methods

### popCard()

`popCard(): Navigation`

Developer Preview: Available as part of the Google Workspace Developer Preview Program, which grants early access to certain features. Available for Google Workspace add-ons that extend Google Chat. Pops a card from the navigation stack. Can be chained with other card navigation actions.

### popToNamedCard(cardName)

`popToNamedCard(cardName: String): Navigation`

Developer Preview: Available as part of the Google Workspace Developer Preview Program, which grants early access to certain features. Available for Google Workspace add-ons that extend Google Chat. Pops to the specified card by its card name. Can be chained with other card navigation actions.

**Parameters**
- `cardName` (String) — The name of the card to navigate to.

### popToRoot()

`popToRoot(): Navigation`

Developer Preview: Available as part of the Google Workspace Developer Preview Program, which grants early access to certain features. Available for Google Workspace add-ons that extend Google Chat. Pops the card stack to the root card. Can be chained with other card navigation actions.

### printJson()

`printJson(): String`

Prints the JSON representation of this object. This is for debugging only.

### pushCard(card)

`pushCard(card: Card): Navigation`

Pushes the given card onto the stack. Can be chained with other card navigation actions.

**Parameters**
- `card` (Card) — A card to add to the stack.

**Code Sample:**
```javascript
const card = CardService.newCardBuilder()
    .setHeader(CardService.newCardHeader().setTitle('Card title'))
    .addSection(cardSection)
    .build();

const navigation = AddOnsResponseService.newNavigation()
    .pushCard(card);
```

### setEndNavigation(endNavigation)

`setEndNavigation(endNavigation: EndNavigation): Navigation`

Sets the end navigation action.

**Parameters**
- `endNavigation` (EndNavigation) — The EndNavigation to use.

**Code Sample:**
```javascript
const navigation = AddOnsResponseService.newNavigation()
    .setEndNavigation(AddOnsResponseService.EndNavigation.CLOSE_DIALOG);
```

### updateCard(card)

`updateCard(card: Card): Navigation`

Does an in-place replacement of the current card. Can be chained with other card navigation actions.

**Parameters**
- `card` (Card) — A card to replace the current card with.

**Code Sample:**
```javascript
const card = CardService.newCardBuilder()
    .setHeader(CardService.newCardHeader().setTitle('Card title'))
    .addSection(cardSection)
    .build();

const navigation = AddOnsResponseService.newNavigation()
    .updateCard(card);
```
