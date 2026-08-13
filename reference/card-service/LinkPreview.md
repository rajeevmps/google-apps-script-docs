# LinkPreview

Card action that displays a link preview card and smart chip in the host app. To use link previews, you must build and return a LinkPreview object in your script.

## Methods

### printJson(): String

Prints the JSON representation of this object. This is for debugging only.

### setLinkPreviewTitle(title: String): LinkPreview

Sets the title that displays in the link preview above the preview card. If unset, the link preview displays the header of the PreviewCard.

Parameters:
- `title` (String) - The title of the link preview.

### setPreviewCard(previewCard: Card): LinkPreview

Sets the card that displays information about a link from a third-party or non-Google service.

Parameters:
- `previewCard` (Card) - The preview card.

### setTitle(title: String): LinkPreview

Sets the title that displays in the smart chip for the link preview. If unset, the smart chip displays the header of the PreviewCard.

Parameters:
- `title` (String) - The title of the smart chip.

```javascript
const decoratedText = CardService.newDecoratedText().setTopLabel('Hello').setText('Hi!');
const cardSection = CardService.newCardSection().addWidget(decoratedText);
const card = CardService.newCardBuilder().addSection(cardSection).build();
return CardService.newLinkPreview().setPreviewCard(card).setTitle('Smart chip title');
```
