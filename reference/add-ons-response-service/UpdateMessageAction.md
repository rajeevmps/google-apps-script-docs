# UpdateMessageAction

The Chat app updates text or cards in a message.

The Chat app updates text or cards in a message. For details, see Send Google Chat messages. Available for Google Workspace add-ons that extend Google Chat.

## Methods

### setMessage(message)

`setMessage(message: ChatMessage): UpdateMessageAction`

Sets the message for this action.

**Parameters**
- `message` (ChatMessage) — The chat message to update.

**Returns**
- `UpdateMessageAction` — This object, for chaining.

## Code Sample

```javascript
const card = CardService.newCardBuilder()
    .setHeader(CardService.newCardHeader().setTitle("Card Title"))
    .addSection(CardService.newCardSection()
      .addWidget(CardService.newTextParagraph().setText("Text paragraph")))
    .build();

const cardWithId = CardService.newCardWithId().setCardId("card_one").setCard(card);

const message = AddOnsResponseService.newChatMessage().addCardWithId(cardWithId);

const chatDataAction = AddOnsResponseService.newChatDataActionBuilder()
    .setUpdateChatMessageAction(AddOnsResponseService.newUpdateMessageAction()
    .setMessage(message))
    .build();
```
