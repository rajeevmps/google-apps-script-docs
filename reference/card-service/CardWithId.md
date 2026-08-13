# CardWithId

A builder for `CardWithId` objects.

A builder for `CardWithId` objects. This class is a unique identifier for a card in a message when sending multiple cards.

Only available for Google Chat apps. Not available for Google Workspace add-ons.

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
```

## Methods

### setCard(card: Card): CardWithId

Sets the card of the `cardWithId`.

Returns: `CardWithId` — This object, for chaining.

### setCardId(id: String): CardWithId

Sets the unique card ID of the `cardWithId`.

Returns: `CardWithId` — This object, for chaining.
