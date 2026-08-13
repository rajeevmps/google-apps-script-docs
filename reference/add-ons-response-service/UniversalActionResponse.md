# UniversalActionResponse

The response object that may be returned from a method that creates universal action.

The response object that may be returned from a method that creates universal action.

## Methods

### printJson()

`printJson(): String`

Prints the JSON representation of this object. This is for debugging only.

## Code Samples

**Example 1 - Opening a Link:**
```javascript
const openLinkUniversalAction =
    AddOnsResponseService.newUniversalActionResponseBuilder()
        .setOpenLink(AddOnsResponseService.newOpenLink().setUrl('https://www.google.com'))
        .build();
```

**Example 2 - Displaying Cards:**
```javascript
const cardBuilder1 = CardService.newCardBuilder();
const cardBuilder2 = CardService.newCardBuilder();
// Finish building the cards ...

const cardsUniversalAction =
    AddOnsResponseService.newUniversalActionResponseBuilder()
        .displayAddOnCards([cardBuilder1.build(), cardBuilder2.build()])
        .build();
```
