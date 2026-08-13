# UniversalActionResponse

The response object that may be returned from a method that creates universal action.

The response object that may be returned from a method that creates universal action. Universal actions can open links or display add-on cards.

## Methods

### printJson(): String

Prints the JSON representation of this object. This is for debugging only.

```javascript
// A universal action that opens a link.
const openLinkUniversalAction =
    CardService.newUniversalActionResponseBuilder()
        .setOpenLink(CardService.newOpenLink().setUrl('https://www.google.com'))
        .build();

const cardBuilder1 = CardService.newCardBuilder();
const cardBuilder2 = CardService.newCardBuilder();
// Finish building the cards ...

// A universal action that shows two static cards.
const cardsUniversalAction =
    CardService.newUniversalActionResponseBuilder()
        .displayAddOnCards([cardBuilder1.build(), cardBuilder2.build()])
        .build();
```
