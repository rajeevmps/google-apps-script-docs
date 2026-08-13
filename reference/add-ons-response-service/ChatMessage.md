# ChatMessage

A Google Chat message.

A Google Chat [message](https://developers.google.com/workspace/chat/api/reference/rest/v1/spaces.messages). Available for Google Workspace add-ons that extend Google Chat.

## Methods

### addAccessoryWidget(accessoryWidget)

`addAccessoryWidget(accessoryWidget: AccessoryWidget): ChatMessage`

Sets the accessoryWidget for this action.

**Parameters**
- `accessoryWidget` (AccessoryWidget) — The accessoryWidget to set.

**Returns**
- `ChatMessage` — This object, for chaining.

### addCardWithId(cardWithId)

`addCardWithId(cardWithId: CardWithId): ChatMessage`

Sets the card of the message.

**Parameters**
- `cardWithId` (CardWithId) — The cardWithId to set.

**Returns**
- `ChatMessage` — This object, for chaining.

**Code Sample:**
```javascript
const card = CardService.newCardBuilder()
    .setHeader(CardService.newCardHeader().setTitle("Card Title"))
    .addSection(CardService.newCardSection()
      .addWidget(CardService.newTextParagraph().setText("Text paragraph")))
    .build();
const cardWithId = CardService.newCardWithId().setCardId("card_one").setCard(card);
const message = AddOnsResponseService.newChatMessage().addCardWithId(cardWithId);
```

### setText(text)

`setText(text: String): ChatMessage`

Sets the text of the message.

**Parameters**
- `text` (String) — The text part of a message.

**Returns**
- `ChatMessage` — This object, for chaining.

**Code Sample:**
```javascript
const message = AddOnsResponseService.newChatMessage().setText("Example text");
```
