# Carousel

Carousel, also known as slider, rotates and displays a list of widgets in a slideshow format.

Carousel, also known as slider, rotates and displays a list of widgets in a slideshow format, with buttons navigating to the previous or next widget.

Available for Google Workspace add-ons and Google Chat apps.

```javascript
const carousel =
    CardService.newCarousel()
        .addCarouselCard(CardService.newCarouselCard().addWidget(
            CardService.newTextParagraph().setText('The first text paragraph in carousel')))
        .addCarouselCard(CardService.newCarouselCard().addWidget(
            CardService.newTextParagraph().setText('The second text paragraph in carousel')))
        .addCarouselCard(CardService.newCarouselCard().addWidget(
            CardService.newTextParagraph().setText('The third text paragraph in carousel')))
```

## Methods

### addCarouselCard(card: CarouselCard): Carousel

Adds a carousel card.

### addEventAction(eventAction: EventAction): Widget

Adds the event action that can be performed on the widget.

### setId(id: String): Widget

Sets the unique ID assigned that's used to identify the widget to be mutated. Widget mutation is only supported in Add-Ons.

### setVisibility(visibility: Visibility): Widget

Sets the visibility of the widget. The default value is `VISIBLE`.
