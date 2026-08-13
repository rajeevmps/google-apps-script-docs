# CreateMessageAction

A builder for Chat `CreateMessageAction` objects.

A builder for Chat `CreateMessageAction` objects. Available for Google Workspace add-ons that extend Google Chat.

## Methods

### setMessage(message)

`setMessage(message: ChatMessage): CreateMessageAction`

Sets the message for this action.

**Parameters**
- `message` (ChatMessage) — The chat message to create.

**Returns**
- `CreateMessageAction` — This object, for chaining.

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
    .setCreateChatMessageAction(AddOnsResponseService.newCreateMessageAction()
    .setMessage(message))
    .build();
```
