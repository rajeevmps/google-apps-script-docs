# MaterialIcon

An object that supports all Google Font Icons. Available for Google Workspace add-ons and Google Chat apps.

## Methods

### setFill(fill: Boolean): MaterialIcon

Whether the icon renders as filled. Default value is `false`. To preview different icon settings, go to Google Font Icons and adjust the settings under Customize.

### setGrade(grade: Integer): MaterialIcon

Weight and grade affect a symbol's thickness. Adjustments to grade are more granular than adjustments to weight and have a small impact on the size of the symbol. Choose from {-25, 0, 200}. If absent, default value is 0. If any other value is specified, the default value is used. To preview different icon settings, go to Google Font Icons and adjust the settings under Customize.

### setName(name: String): MaterialIcon

Sets the name of the icon. Required. The icon name defined in Google Font Icon, For example, `check_box`. Any invalid names are abandoned and replaced with an empty string and results in the icon failing to render.

### setWeight(weight: Integer): MaterialIcon

The stroke weight of the icon. Choose from {100, 200, 300, 400, 500, 600, 700}. If absent, default value is 400. If any other value is specified, the default value is used. To preview different icon settings, go to Google Font Icons and adjust the settings under Customize.

```javascript
const materialIcon = CardService.newMaterialIcon()
                         .setName('search')
                         .setFill(true)
                         .setWeight(400)
                         .setGrade(0);
```
