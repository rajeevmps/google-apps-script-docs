# IconImage

A predefined icon, a material design icon, or an icon from a URL with a customizable crop style.

IconImage allows you to use a predefined icon, a material design icon, or an icon from a URL with customizable crop style. You can set alternative text for accessibility, choose from predefined icons, specify an icon URL, set the image crop type, and set a material design icon.

## Methods

### setAltText(altText: String): IconImage

Sets the alternative text of the URL which is used for accessibility.

### setIcon(icon: Icon): IconImage

Sets the predefined icon if the URL is not set. Default is NONE.

### setIconUrl(url: String): IconImage

Sets the URL of the icon if the icon is not set.

### setImageCropType(imageCropType: ImageCropType): IconImage

Sets the crop style for the image. The crop type options you can use for icons are `SQUARE` and `CIRCLE`. Default is `SQUARE`.

### setMaterialIcon(icon: MaterialIcon): IconImage

Sets the material design icon.

```javascript
const iconImage = CardService.newIconImage().setMaterialIcon(
    CardService.newMaterialIcon().setName('search'),
);
```
