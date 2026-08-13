# ChatResponse

The response object for a card message in Google Chat.

The response object for a card message in Google Chat. Only available for Google Chat apps. Not available for Google Workspace add-ons.

```javascript
// Creates a card message in Chat.
const cardHeader = CardService.newCardHeader()
                       .setTitle('Card Header Title')
                       .setSubtitle('Card Header Subtitle');

const card = CardService.newCardBuilder().setHeader(cardHeader).build();

const chatResponse =
    CardService.newChatResponseBuilder()
        .setText('Example text')
        .addCardsV2(
            CardService.newCardWithId().setCardId('card_id').setCard(card))
        .build();

console.log(chatResponse.printJson());
```

## Methods

### printJson(): String

Prints the JSON representation of this object. This is for debugging only.
