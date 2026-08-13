# GridItem

The items users interact with within a grid widget. Available for Google Workspace add-ons and Google Chat apps.

## Methods

### setIdentifier(id: String): GridItem

Sets the identifier for the grid item. When a user clicks this grid item, this ID is returned in the parent grid's on_click call back parameters.

### setImage(image: ImageComponent): GridItem

Sets the image for this grid item.

### setLayout(layout: GridItemLayout): GridItem

Sets the layout of text and image for the grid item. Default is TEXT_BELOW

### setSubtitle(subtitle: String): GridItem

Sets the subtitle of the grid item.

### setTextAlignment(alignment: HorizontalAlignment): GridItem

Sets the horizontal alignment of the grid item. Default is START.

### setTitle(title: String): GridItem

Sets the title text of the grid item.

```javascript
const gridItem = CardService.newGridItem()
                     .setIdentifier('itemA')
                     .setTitle('This is a cat')
                     .setImage(CardService.newImageComponent())
                     .setLayout(CardService.GridItemLayout.TEXT_BELOW);
```
