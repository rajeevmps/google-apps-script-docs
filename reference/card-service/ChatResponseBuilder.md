# ChatResponseBuilder

A builder for `ChatResponse` objects.

A builder for `ChatResponse` objects. Only available for Google Chat apps. Not available for Google Workspace add-ons.

## Methods

### addCardsV2(cardWithId: CardWithId): ChatResponseBuilder

Sets the card field of the message. This is used to send a card in a Google Chat message. Each card is associated with a unique id, `CardWithId` object should be built and be used with this method.

```javascript
const cardSection = CardService.newCardSection();
cardSection.addWidget(
    CardService.newTextParagraph().setText('This is a text paragraph widget.'),
);

const card = CardService.newCardBuilder()
                 .setHeader(CardService.newCardHeader().setTitle('Card title'))
                 .addSection(cardSection)
                 .build();

const cardWithId =
    CardService.newCardWithId().setCardId('card_id').setCard(card);

const chatResponse =
    CardService.newChatResponseBuilder().addCardsV2(cardWithId).build();
```

### build(): ChatResponse

Builds the current action response and validates it.

### setActionResponse(actionResponse: ChatActionResponse): ChatResponseBuilder

Sets the action response field of the message.

```javascript
const card = CardService.newCardBuilder()
                 .setHeader(CardService.newCardHeader().setTitle('card title'))
                 .build();

const dialog = CardService.newDialog().setBody(card);

const dialogAction = CardService.newDialogAction().setDialog(dialog);

const actionResponse = CardService.newChatActionResponse()
                           .setDialogAction(dialogAction)
                           .setResponseType(CardService.Type.DIALOG);

const chatResponse = CardService.newChatResponseBuilder()
                         .setActionResponse(actionResponse)
                         .build();
```

### setText(text: String): ChatResponseBuilder

Sets the text of the Chat message.

```javascript
const chatResponse =
    CardService.newChatResponseBuilder().setText('Example text').build();
```
