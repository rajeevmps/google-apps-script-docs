# CarouselCard

A card that can be displayed as a carousel item.

A card that can be displayed as a carousel item. Available for Google Workspace add-ons and Google Chat apps.

```javascript
const carouselCard = CardService.newCarouselCard()
    .addWidget(
        CardService.newTextParagraph().setText('a text paragraph in the carousel card'))
    .addFooterWidget(
        CardService.newTextParagraph().setText('a text paragraph in the carousel card footer'));
```

## Methods

### addFooterWidget(widget: Widget): CarouselCard

Adds the given widget to the footer of this carousel card. Widgets are shown in the order they were added.

Parameters: `widget` (Widget) — A widget to add to the footer of the carousel card.

Returns: This object, for chaining.

### addWidget(widget: Widget): CarouselCard

Adds the given widget to this carousel card. Widgets are shown in the order they were added.

Parameters: `widget` (Widget) — A widget to add to the carousel card.

Returns: This object, for chaining.
