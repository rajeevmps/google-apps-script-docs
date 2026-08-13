# Card

A context card that represents a single view in the UI.

A context card that represents a single view in the UI. Cards are built using the `CardService.newCardBuilder()` method and can have sections added using `addSection()`. The `printJson()` method is available for debugging the JSON representation of the Card object.

```javascript
const cardSection = CardService.newCardSection();
// Finish building the card section ...

const card = CardService.newCardBuilder()
                 .setName('Card name')
                 .setHeader(CardService.newCardHeader().setTitle('Card title'))
                 .addSection(cardSection)
                 .build();
```

## Methods

### printJson(): String

Prints the JSON representation of this object. This is for debugging only.
