# StyledText

Text element with styles such as bold, italic and color.

Text element with styles such as bold, italic and color. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### addStyle(style)

`addStyle(style: TextStyle): StyledText`

Sets the style of the styled text, can apply multiple styles to a single styled text.

### setColor(color)

`setColor(color: Color): StyledText`

Sets the color of the styled text.

### setFontWeight(fontWeight)

`setFontWeight(fontWeight: FontWeight): StyledText`

Sets the font weight of the styled text.

### setText(text)

`setText(text: String): StyledText`

Sets the main content of the styled text.

## Code Sample

```javascript
const styledText = AddOnsResponseService.newStyledText()
  .setText("Styled Text!")
  .addStyle(AddOnsResponseService.TextStyle.ITALIC)
  .addStyle(AddOnsResponseService.TextStyle.UNDERLINE)
  .setFontWeight(AddOnsResponseService.FontWeight.BOLD)
  .setColor(
    AddOnsResponseService.newColor()
      .setRed(0.1)
      .setBlue(0.3)
      .setGreen(0.1)
      .setAlpha(0.78)
  );
```
