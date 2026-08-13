# Attribute

An enumeration of the element attributes.

To call an enum, you call its parent class, name, and property. For example, `DocumentApp.Attribute.BACKGROUND_COLOR`.

## Example

```javascript
// Define a style with yellow background.
const highlightStyle = {};
highlightStyle[DocumentApp.Attribute.BACKGROUND_COLOR] = '#FFFF00';
highlightStyle[DocumentApp.Attribute.BOLD] = true;

// Insert "Hello", highlighted.
DocumentApp.getActiveDocument()
    .getActiveTab()
    .asDocumentTab()
    .editAsText()
    .insertText(0, 'Hello\n')
    .setAttributes(0, 4, highlightStyle);
```

## Properties

| Property | Description |
|----------|-------------|
| `BACKGROUND_COLOR` | The background color of an element (Paragraph, Table, etc) or document. |
| `BOLD` | The font weight setting, for rich text. |
| `BORDER_COLOR` | The border color, for table elements. |
| `BORDER_WIDTH` | The border width in points, for table elements. |
| `CODE` | The code contents, for equation elements. |
| `FONT_FAMILY` | The font family setting, for rich text. |
| `FONT_SIZE` | The font size setting in points, for rich text. |
| `FOREGROUND_COLOR` | The foreground color setting, for rich text. |
| `HEADING` | The heading type, for paragraph elements (for example, `DocumentApp.ParagraphHeading.HEADING1`). |
| `HEIGHT` | The height setting, for image elements. |
| `HORIZONTAL_ALIGNMENT` | The horizontal alignment, for paragraph elements (for example, `DocumentApp.HorizontalAlignment.CENTER`). |
| `INDENT_END` | The end indentation setting in points, for paragraph elements. |
| `INDENT_FIRST_LINE` | The first line indentation setting in points, for paragraph elements. |
| `INDENT_START` | The start indentation setting in points, for paragraph elements. |
| `ITALIC` | The font style setting, for rich text. |
| `GLYPH_TYPE` | The glyph type, for list item elements. |
| `LEFT_TO_RIGHT` | The text direction setting, for rich text. |
| `LINE_SPACING` | The line spacing setting as a multiplier, for paragraph elements. |
| `LINK_URL` | The link URL, for rich text. The default link style (foreground color, underline) is automatically applied. |
| `LIST_ID` | The ID of the encompassing list, for list item elements. |
| `MARGIN_BOTTOM` | The bottom margin setting in points, for paragraph elements. |
| `MARGIN_LEFT` | The left margin setting in points, for paragraph elements. |
| `MARGIN_RIGHT` | The right margin setting in points, for paragraph elements. |
| `MARGIN_TOP` | The top margin setting in points, for paragraph elements. |
| `NESTING_LEVEL` | The item nesting level, for list item elements. |
| `MINIMUM_HEIGHT` | The minimum height setting in points, for table row elements. |
| `PADDING_BOTTOM` | The bottom padding setting in points, for table cell elements. |
| `PADDING_LEFT` | The left padding setting in points, for table cell elements. |
| `PADDING_RIGHT` | The right padding setting in points, for table cell elements. |
| `PADDING_TOP` | The top padding setting in points, for table cell elements. |
| `PAGE_HEIGHT` | The page height setting in points, for documents. |
| `PAGE_WIDTH` | The page width setting in points, for documents. |
| `SPACING_AFTER` | The bottom spacing setting in points, for paragraph elements. |
| `SPACING_BEFORE` | The top spacing setting in points, for paragraph elements. |
| `STRIKETHROUGH` | The strike-through setting, for rich text. |
| `UNDERLINE` | The underline setting, for rich text. |
| `VERTICAL_ALIGNMENT` | The vertical alignment setting, for table cell elements. |
| `WIDTH` | The width setting, for table cell and image elements. |
