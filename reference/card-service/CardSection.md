# CardSection

A card section holds groups of widgets and provides visual separation between them.

A card section holds groups of widgets and provides visual separation between them. Available for Google Workspace add-ons and Google Chat apps.

```javascript
const image = CardService.newImage();
// Build image ...
const textParagraph = CardService.newTextParagraph();
// Build text paragraph ...

const cardSection = CardService.newCardSection()
                        .setHeader('Section header')
                        .addWidget(image)
                        .addWidget(textParagraph);
```

## Methods

### addWidget(widget: Widget): CardSection

Adds the given widget to this section. Widgets are shown in the order they were added. You can't add more than 100 widgets to a card section.

### setCollapseControl(collapseControl: CollapseControl): CardSection

Sets the customizable expand and collapse buttons of the section. These buttons are shown only if the section is collapsible. If this field isn't set, default buttons are used. Available for Google Chat apps. In developer preview for Google Workspace add-ons.

### setCollapsible(collapsible: Boolean): CardSection

Sets whether the section can be collapsed.

### setHeader(header: String): CardSection

Sets the header of the section. Optional.

### setId(id: String): CardSection

Sets the unique ID assigned that's used to identify the section to be mutated. Section mutation is only supported in Add-Ons.

### setNumUncollapsibleWidgets(numUncollapsibleWidgets: Integer): CardSection

Sets the number of widgets that are still shown when this section is collapsed. The widgets shown are always the first ones that were added.
