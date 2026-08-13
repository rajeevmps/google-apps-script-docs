# TextStyle

The style of text.

The style of text.

Read methods in this class return null if the corresponding TextRange spans multiple text runs, and those runs have different values for the read method being called. To avoid this, query for text styles using the TextRanges returned by the TextRange.getRuns() method.

If you use methods that edit how text fits within a shape, any autofit settings applied to the text styles are deactivated.

## Methods

### getBackgroundColor()

`Color|null`

Returns the background color of the text, or null if there are multiple styles on the text.

**Returns**

`Color|null` — The background color of the text.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getBaselineOffset()

`TextBaselineOffset|null`

Returns the vertical offset of text from its normal position, or null if there are multiple styles on the text.

**Returns**

`TextBaselineOffset|null` — The vertical offset of text from its normal position.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getFontFamily()

`String|null`

Returns the font family of the text, or null if there are multiple styles on the text.

**Returns**

`String|null` — The font family of the text.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getFontSize()

`Number|null`

Returns the font size of the text in points, or null if there are multiple styles on the text.

**Returns**

`Number|null` — The font size of the text in points.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getFontWeight()

`Integer|null`

Returns the font weight of the text, or null if there are multiple styles on the text.

The weight is a multiple of 100 between 100 and 900, inclusive. This range corresponds to the numerical values described in the CSS 2.1 Specification, section 15.6, with non-numerical values disallowed. Weights greater than or equal to 700 are considered bold, in which case isBold() returns true. The default value is 400 ("normal").

**Returns**

`Integer|null` — The font weight of the text.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getForegroundColor()

`Color|null`

Returns the foreground color of the text, or null if there are multiple styles on the text.

**Returns**

`Color|null` — The foreground color of the text.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getLink()

`Link|null`

Returns the Link on the text, or null if there is no link or if the link is on part of the text or if there are multiple links. Call hasLink() to determine whether the text has no link.

```javascript
const shape = SlidesApp.getActivePresentation().getSlides()[0].getShapes()[0];
const textLink = shape.getText().getTextStyle().getLink();
if (textLink != null) {
  Logger.log(`Shape text has a link of type: ${textLink.getLinkType()}`);
}
```

**Returns**

`Link|null` — The link on the text.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### hasLink()

`Boolean|null`

Returns true if there is link on the text, false if not, or null if the link is on part of the text or there are multiple links.

Links cannot be set on newline characters. Therefore, if the TextRange contains a newline character, this method always returns either null or false.

**Returns**

`Boolean|null` — Whether there is a link on the text.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### isBackgroundTransparent()

`Boolean|null`

Returns true if the background of the text is transparent, false if not, or null if there are multiple styles on the text.

**Returns**

`Boolean|null` — Whether the background of the text is transparent.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### isBold()

`Boolean|null`

Returns true if the text is rendered as bold, false if not, or null if there are multiple styles on the text.

**Returns**

`Boolean|null` — Whether the text is rendered as bold.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### isItalic()

`Boolean|null`

Returns true if the text is italicized, false if not, or null if there are multiple styles on the text.

**Returns**

`Boolean|null` — Whether the text is italicized.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### isSmallCaps()

`Boolean|null`

Returns true if the text is in small capital letters, false if not, or null if there are multiple styles on the text.

**Returns**

`Boolean|null` — Whether the text is in small capital letters.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### isStrikethrough()

`Boolean|null`

Returns true if the text is struck through, false if not, or null if there are multiple styles on the text.

**Returns**

`Boolean|null` — Whether the text is struck through.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### isUnderline()

`Boolean|null`

Returns true if the text is underlined, false if not, or null if there are multiple styles on the text.

**Returns**

`Boolean|null` — Whether the text is underlined.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### removeLink()

`TextStyle`

Removes a Link.

Removing a link removes the hyperlink foreground color and underline style on the text. If possible, these styles are applied to match the text preceding the link.

```javascript
const textRange = SlidesApp.getActivePresentation().getSlides()[0].getShapes()[0].getText();
textRange.getTextStyle().removeLink();
```

**Returns**

`TextStyle` — This TextStyle, for chaining.

### setBackgroundColor(color)

`TextStyle`

Sets the background color of the text.

**Parameters**

- `color` (`Color`) — The background color to set.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setBackgroundColor(red, green, blue)

`TextStyle`

Sets the background color of the text to the given RGB values from 0 to 255.

**Parameters**

- `red` (`Integer`) — The red component of the color.
- `green` (`Integer`) — The green component of the color.
- `blue` (`Integer`) — The blue component of the color.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setBackgroundColor(hexColor)

`TextStyle`

Sets the background color of the text to the given hex color string.

The hex string must be in the format '#RRGGBB'. For example, pink is represented as

**Parameters**

- `hexColor` (`String`) — The hex color string.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setBackgroundColor(color)

`TextStyle`

Sets the background color of the text to the given ThemeColorType.

**Parameters**

- `color` (`ThemeColorType`) — The theme color type.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setBackgroundColorTransparent()

`TextStyle`

Sets the background color of the text to transparent.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setBaselineOffset(offset)

`TextStyle`

Sets the vertical offset of the text relative to its normal position.

**Parameters**

- `offset` (`TextBaselineOffset`) — The baseline offset to set.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setBold(bold)

`TextStyle`

Sets whether the text should be rendered as bold.

**Parameters**

- `bold` (`Boolean`) — Whether to render the text as bold.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setFontFamily(fontFamily)

`TextStyle`

Sets the font family of the text .

**Parameters**

- `fontFamily` (`String`) — The font family to set.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setFontFamilyAndWeight(fontFamily, fontWeight)

`TextStyle`

Sets the font family and weight of the text.

**Parameters**

- `fontFamily` (`String`) — The font family.
- `fontWeight` (`Integer`) — The font weight.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setFontSize(fontSize)

`TextStyle`

Sets the font size of the text, in points.

**Parameters**

- `fontSize` (`Number`) — The font size in points.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setForegroundColor(foregroundColor)

`TextStyle`

Sets the foreground color of the text.

**Parameters**

- `foregroundColor` (`Color`) — The foreground color to set.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setForegroundColor(red, green, blue)

`TextStyle`

Sets the foreground color of the text to the given RGB values from 0 to 255.

**Parameters**

- `red` (`Integer`) — The red component of the color.
- `green` (`Integer`) — The green component of the color.
- `blue` (`Integer`) — The blue component of the color.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setForegroundColor(hexColor)

`TextStyle`

Sets the foreground color of the text to the given hex color string.

The hex string must be in the format '#RRGGBB'. For example, pink is represented as

**Parameters**

- `hexColor` (`String`) — The hex color string.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setForegroundColor(color)

`TextStyle`

Sets the foreground color of the text to the given ThemeColorType.

**Parameters**

- `color` (`ThemeColorType`) — The theme color type.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setItalic(italic)

`TextStyle`

Sets the whether the text is italicized.

**Parameters**

- `italic` (`Boolean`) — Whether to render the text as italic.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setLinkSlide(slideIndex)

`TextStyle`

Sets a Link to the given Slide using the zero-based index of the slide.

Setting a link changes the style of the text to be underlined and to have a ThemeColorType.HYPERLINK foreground color. This can be changed via setForegroundColor(hexColor) and setUnderline(underline).

Since links cannot be set on newline characters, newline characters in the TextRange are ignored.

```javascript
// Set a link to the first slide of the presentation.
const presentation = SlidesApp.getActivePresentation();
const slide = presentation.getSlides()[0];
const textRange = slide.getShapes()[0].getText();
textRange.getTextStyle().setLinkSlide(0);
```

**Parameters**

- `slideIndex` (`Integer`) — The zero-based index to the slide.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setLinkSlide(slide)

`TextStyle`

Sets a Link to the given Slide, the link is set by the given slide ID.

Setting a link changes the style of the text to be underlined and to have a ThemeColorType.HYPERLINK foreground color. This can be changed via setForegroundColor(hexColor) and setUnderline(underline).

Since links cannot be set on newline characters, newline characters in the TextRange are ignored.

```javascript
// Set a link to the first slide of the presentation.
const presentation = SlidesApp.getActivePresentation();
const slide = presentation.getSlides()[0];
const textRange = slide.getShapes()[0].getText();
textRange.getTextStyle().setLinkSlide(slide);
```

**Parameters**

- `slide` (`Slide`) — The Slide to be linked.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setLinkSlide(slidePosition)

`TextStyle`

Sets a Link to the given Slide using the relative position of the slide.

Setting a link changes the style of the text to be underlined and to have a ThemeColorType.HYPERLINK foreground color. This can be changed via setForegroundColor(hexColor) and setUnderline(underline).

Since links cannot be set on newline characters, newline characters in the TextRange are ignored.

```javascript
// Set a link to the first slide of the presentation.
const textRange = SlidesApp.getActivePresentation().getSlides()[0].getShapes()[0].getText();
textRange.getTextStyle().setLinkSlide(SlidesApp.SlidePosition.FIRST_SLIDE);
```

**Parameters**

- `slidePosition` (`SlidePosition`) — The relative SlidePosition.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setLinkUrl(url)

`TextStyle`

Sets a Link to the given non-empty URL string.

Setting a link changes the style of the text to be underlined and to have a ThemeColorType.HYPERLINK foreground color. This can be changed via setForegroundColor(hexColor) and setUnderline(underline).

Since links cannot be set on newline characters, newline characters in the TextRange are ignored.

```javascript
// Set a link to the URL.
const textRange = SlidesApp.getActivePresentation().getSlides()[0].getShapes()[0].getText();
textRange.getTextStyle().setLinkUrl('https://slides.google.com');
```

**Parameters**

- `url` (`String`) — The URL string.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setSmallCaps(smallCaps)

`TextStyle`

Sets whether the text is rendered in small capital letters.

**Parameters**

- `smallCaps` (`Boolean`) — Whether to render the text in small capital letters.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setStrikethrough(strikethrough)

`TextStyle`

Sets whether the text is struck through.

**Parameters**

- `strikethrough` (`Boolean`) — Whether to strike through the text.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setUnderline(underline)

`TextStyle`

Sets whether the text is underlined.

**Parameters**

- `underline` (`Boolean`) — Whether to underline the text.

**Returns**

`TextStyle` — This TextStyle, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

## Properties

This class has no properties listed on the reference page.
