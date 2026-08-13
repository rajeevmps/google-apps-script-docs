# RichTextValueBuilder

A builder for Rich Text values.

A builder for Rich Text values.

## Methods

### `build()`

Creates a Rich Text value from this builder.

**Returns:** RichTextValue — A Rich Text value created from this builder.

### `setLinkUrl(startOffset, endOffset, linkUrl)`

Sets the link URL for the given substring of this value, or clears it if linkUrl is null .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| start Offset | Integer | The start offset for the substring, inclusive. |
| end Offset | Integer | The end offset for the substring, exclusive. |
| link Url | String | The link URL being set. |

**Returns:** RichTextValueBuilder — This builder, for chaining.

```javascript
// Creates a Rich Text value for the text "foo no baz" with "foo" pointing to
// "https://bar.foo" and "baz" to "https://abc.xyz".
// "foo" is underlined with the default link color, whereas "baz" has its text
// style overridden by a call to `setTextStyle`, and is therefore black and bold
// with no underlining.
const boldStyle = SpreadsheetApp.newTextStyle()
                      .setUnderline(false)
                      .setBold(true)
                      .setForegroundColor('#000000')
                      .build();
const value = SpreadsheetApp.newRichTextValue()
                  .setText('foo no baz')
                  .setLinkUrl(0, 3, 'https://bar.foo')
                  .setLinkUrl(7, 10, 'https://abc.xyz')
                  .setTextStyle(7, 10, boldStyle)
                  .build();
```

### `setLinkUrl(linkUrl)`

Sets the link URL for the entire value, or clears it if linkUrl is null .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| link Url | String | The link URL being set. |

**Returns:** RichTextValueBuilder — This builder, for chaining.

```javascript
// Creates a Rich Text value for the text "Foo" which points to
// "https://bar.foo".
const value = SpreadsheetApp.newRichTextValue()
                  .setText('Foo')
                  .setLinkUrl('https://bar.foo')
                  .build();
```

### `setText(text)`

Sets the text for this value and clears any existing text style. When creating a new Rich Text
value, this should be called before setTextStyle(startOffset, endOffset, textStyle) .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| text | String | The text for this value. |

**Returns:** RichTextValueBuilder — This builder, for chaining.

### `setTextStyle(startOffset, endOffset, textStyle)`

Applies a text style to the given substring of this value. Offsets are 0 based and are relative
to the cell's text value. Does nothing if textStyle is null .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| start Offset | Integer | The start offset for the substring, inclusive. |
| end Offset | Integer | The end offset for the substring, exclusive. |
| text Style | Text Style | The text style being set. |

**Returns:** RichTextValueBuilder — This builder, for chaining.

```javascript
// Creates a Rich Text value for the text "HelloWorld", with "Hello" bolded, and
// "World" italicized.
const bold = SpreadsheetApp.newTextStyle().setBold(true).build();
const italic = SpreadsheetApp.newTextStyle().setItalic(true).build();
const value = SpreadsheetApp.newRichTextValue()
                  .setText('HelloWorld')
                  .setTextStyle(0, 5, bold)
                  .setTextStyle(5, 10, italic)
                  .build();
```

### `setTextStyle(textStyle)`

Applies a text style to the entire value. Previously set text styles are only affected if they
are directly overwritten by values within textStyle . Does nothing if textStyle is null .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| text Style | Text Style | The text style being set. |

**Returns:** RichTextValueBuilder — This builder, for chaining.

```javascript
// Creates a Rich Text value for the text "HelloWorld" with "Hello" bolded and
// italicized, and "World" only italicized.
const bold = SpreadsheetApp.newTextStyle().setBold(true).build();
const italic = SpreadsheetApp.newTextStyle().setItalic(true).build();
const value = SpreadsheetApp.newRichTextValue()
                  .setText('HelloWorld')
                  .setTextStyle(0, 5, bold)
                  .setTextStyle(italic)
                  .build();
```

