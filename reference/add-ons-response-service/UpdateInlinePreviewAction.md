# UpdateInlinePreviewAction

The Chat app previews a link in a message by adding or updating one or more cards.

The Chat app previews a link in a message by adding or updating one or more cards. For details, see Preview links in Google Chat messages. Available for Google Workspace add-ons that extend Google Chat.

## Methods

### addCardWithId(cardWithId)

`addCardWithId(cardWithId: CardWithId): UpdateInlinePreviewAction`

Adds the card for this action.

**Parameters**
- `cardWithId` (CardWithId) — The card to be set.

**Returns**
- `UpdateInlinePreviewAction` — This object, for chaining.

### addExpiration(ttl)

`addExpiration(ttl: Integer): UpdateInlinePreviewAction`

Adds the expiration for this action.

**Parameters**
- `ttl` (Integer) — The duration of expiration to be set.

**Returns**
- `UpdateInlinePreviewAction` — This object, for chaining.

## Code Sample

```javascript
const card = CardService.newCardBuilder()
    .setHeader(CardService.newCardHeader().setTitle("Unfurl Card!"))
    .addSection(CardService.newCardSection()
      .addWidget(CardService.newTextParagraph().setText("url"))
      .addWidget(CardService.newButtonSet()
        .addButton(CardService.newTextButton()
          .setText("Open URL!")
          .setOpenLink(CardService.newOpenLink().setUrl("https://www.google.com")))))
    .build();

const cardWithId = CardService.newCardWithId().setCardId("card_one").setCard(card);

const chatDataAction = AddOnsResponseService.newChatDataActionBuilder()
    .setUpdateInlinePreviewAction(AddOnsResponseService.newUpdateInlinePreviewAction()
    .addCardWithId(cardWithId)).build();
```
