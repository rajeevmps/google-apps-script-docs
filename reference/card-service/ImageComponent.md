# ImageComponent

An image component that can be added to grid items.

Available for Google Workspace add-ons and Google Chat apps.

## Methods

### setAltText(altText: String): ImageComponent

Sets the alternative text of the image.

Parameters:
- `altText` (String) - The alt_text to set for the image.

### setBorderStyle(borderStyle: BorderStyle): ImageComponent

Sets the border style applied to the image.

Parameters:
- `borderStyle` (BorderStyle) - The BorderStyle object to apply.

### setCropStyle(imageCropStyle: ImageCropStyle): ImageComponent

Sets the crop style for the image.

Parameters:
- `imageCropStyle` (ImageCropStyle) - The ImageCropStyle object to apply.

### setImageUrl(url: String): ImageComponent

Sets the URL of the image.

Parameters:
- `url` (String) - The URL.

```javascript
const ImageComponent = CardService.newImageComponent()
                           .setImageUrl('http://imageurl.ca')
                           .setAltText('YOUR ALT TEXT')
                           .setCropStyle(CardService.newImageCropStyle())
                           .setBorderStyle(CardService.newBorderStyle());
```
