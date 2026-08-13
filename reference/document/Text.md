# Text

An element representing a rich text region.

All text in a `Document` is contained within `Text` elements. A `Text` element can be contained within an `Equation`, `EquationFunction`, `ListItem`, or `Paragraph`, but cannot itself contain any other element.

Scripts that use these methods require authorization with one or more of the following scopes: `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`.

## Example

```javascript
// Gets the body contents of the active tab.
const body = DocumentApp.getActiveDocument().getActiveTab()
  .asDocumentTab().getBody();

// Use editAsText to obtain a single text element containing
// all the characters in the tab.
const text = body.editAsText();

// Insert text at the beginning of the tab.
text.insertText(0, 'Inserted text.\n');

// Insert text at the end of the tab.
text.appendText('\nAppended text.');

// Make the first half of the tab blue.
text.setForegroundColor(0, text.getText().length / 2, '#00FFFF');
```

```javascript
// Opens the Docs file by its URL. If you created your script from within a
// Google Docs file, you can use DocumentApp.getActiveDocument() instead.
// TODO(developer): Replace the URL with your own.
const doc = DocumentApp.openByUrl(
    'https://docs.google.com/document/d/DOCUMENT_ID/edit',
);

// Gets the body contents of the tab by its ID.
// TODO(developer): Replace the ID with your own.
const body = doc.getTab('123abc').asDocumentTab().getBody();

// Sets the font of the first 16 characters to Impact.
const text = body.editAsText().setFontFamily(0, 15, 'Impact');

// Gets the font family of the 16th character in the tab body.
const fontFamily = text.getFontFamily(15);

// Logs the font family to the console.
console.log(fontFamily);
```

```javascript
const body = DocumentApp.getActiveDocument().getActiveTab()
  .asDocumentTab().getBody();

// Insert two paragraphs separated by a paragraph containing an
// horizontal rule.
body.insertParagraph(0, 'An editAsText sample.');
body.insertHorizontalRule(0);
body.insertParagraph(0, 'An example.');

// Delete " sample.\n\n An" removing the horizontal rule in the process.
body.editAsText().deleteText(14, 25);
```

```javascript
const doc = DocumentApp.getActiveDocument();
const documentTab = doc.getActiveTab().asDocumentTab();
const body = documentTab.getBody();

// Append a styled paragraph.
const par = body.appendParagraph('A bold, italicized paragraph.');
par.setBold(true);
par.setItalic(true);

// Retrieve the paragraph's attributes.
const atts = par.getAttributes();

// Log the paragraph attributes.
for (const att in atts) {
  Logger.log(`${att}:${atts[att]}`);
}
```

```javascript
// Opens the Docs file by its URL. If you created your script from within a
// Google Docs file, you can use DocumentApp.getActiveDocument() instead.
// TODO(developer): Replace the URL with your own.
const doc = DocumentApp.openByUrl(
    'https://docs.google.com/document/d/DOCUMENT_ID/edit',
);

// Gets the body contents of the tab by its ID.
// TODO(developer): Replace the ID with your own.
const body = doc.getTab('123abc').asDocumentTab().getBody();

// Declares style attributes.
const style = {};
style[DocumentApp.Attribute.BOLD] = true;
style[DocumentApp.Attribute.ITALIC] = true;
style[DocumentApp.Attribute.FONT_SIZE] = 29;

// Sets the style attributes to the tab's body.
const text = body.editAsText();
text.setAttributes(style);

// Gets the style attributes applied to the eleventh character in the
// body and logs them to the console.
const attributes = text.getAttributes(10);
console.log(attributes);
```

```javascript
// Opens the Docs file by its URL. If you created your script from within a
// Google Docs file, you can use DocumentApp.getActiveDocument() instead.
// TODO(developer): Replace the URL with your own.
const doc = DocumentApp.openByUrl(
    'https://docs.google.com/document/d/DOCUMENT_ID',
);

// Gets the body contents of the tab by its ID.
// TODO(developer): Replace the ID with your own.
const body = doc.getTab('123abc').asDocumentTab().getBody();

// Sets the background color of the first 3 characters in the body.
const text = body.editAsText().setBackgroundColor(0, 2, '#FFC0CB');

// Gets the background color of the first character in the body.
const backgroundColor = text.getBackgroundColor(0);

// Logs the background color to the console.
console.log(backgroundColor);
```

## Methods

### appendText(text String)

Returns: Text

Adds the specified text to the end of this text region.

### copy()

Returns: Text

Returns a detached, deep copy of the current element. Any child elements present in the element are also copied. The new element doesn't have a parent.

### deleteText(startOffset Integer, endOffsetInclusive Integer)

Returns: Text

Deletes a range of text.

### editAsText()

Returns: Text

Obtains a Text version of the current element, for editing. Use `editAsText` for manipulating the elements contents as rich text. The `editAsText` mode ignores non-text elements (such as InlineImage and HorizontalRule). Child elements fully contained within a deleted text range are removed from the element.

### findText(searchPattern String)

Returns: RangeElement | null

Searches the contents of the element for the specified text pattern using regular expressions. A subset of the JavaScript regular expression features are not fully supported, such as capture groups and mode modifiers. The provided regular expression pattern is independently matched against each text block contained in the current element.

### findText(searchPattern String, from RangeElement)

Returns: RangeElement | null

Searches the contents of the element for the specified text pattern, starting from a given search result. A subset of the JavaScript regular expression features are not fully supported, such as capture groups and mode modifiers. The provided regular expression pattern is independently matched against each text block contained in the current element.

### getAttributes()

Returns: Object

Retrieves the element's attributes. The result is an object containing a property for each valid element attribute where each property name corresponds to an item in the `DocumentApp.Attribute` enumeration.

### getAttributes(offset Integer)

Returns: Object

Retrieves the attributes at the specified character offset. The result is an object containing a property for each valid text attribute where each property name corresponds to an item in the `DocumentApp.Attribute` enumeration.

### getBackgroundColor()

Returns: String | null

Retrieves the background color setting. Returns the background color, formatted in CSS notation (like `'#ffffff'`), or null if the element contains multiple values for this attribute.

### getBackgroundColor(offset Integer)

Returns: String | null

Retrieves the background color at the specified character offset. Returns the background color, formatted in CSS notation (like `'#ffffff'`).

### getFontFamily()

Returns: String | null

Retrieves the font family setting. The name can be any font from the Font menu in Docs or Google Fonts, and is case-sensitive. The methods `getFontFamily()` and `setFontFamily(fontFamilyName)` now use string names for fonts instead of the `FontFamily` enum. Although this enum is deprecated, it will remain available for compatibility with older scripts.

### getFontFamily(offset Integer)

Returns: String | null

Retrieves the font family at the specified character offset. The name can be any font from the Font menu in Docs or Google Fonts, and is case-sensitive. The methods `getFontFamily()` and `setFontFamily(fontFamilyName)` now use string names for fonts instead of the `FontFamily` enum. Although this enum is deprecated, it will remain available for compatibility with older scripts.

### getFontSize()

Returns: Number | null

Retrieves the font size setting.

### getFontSize(offset Integer)

Returns: Number | null

Retrieves the font size at the specified character offset.

### getForegroundColor()

Returns: String | null

Retrieves the foreground color setting.

### getForegroundColor(offset Integer)

Returns: String | null

Retrieves the foreground color at the specified character offset.

### getLinkUrl()

Returns: String | null

Retrieves the link url.

### getLinkUrl(offset Integer)

Returns: String | null

Retrieves the link URL at the specified character offset.

### getNextSibling()

Returns: Element | null

Retrieves the element's next sibling element.

### getParent()

Returns: ContainerElement | null

Retrieves the element's parent element.

### getPreviousSibling()

Returns: Element | null

Retrieves the element's previous sibling element.

### getText()

Returns: String

Retrieves the contents of the element as a text string.

### getTextAlignment()

Returns: TextAlignment | null

Gets the text alignment.

### getTextAlignment(offset Integer)

Returns: TextAlignment | null

Gets the text alignment for a single character.

### getTextAttributeIndices()

Returns: Integer[]

Retrieves the set of text indices that correspond to the start of distinct text formatting runs.

### getType()

Returns: ElementType

Retrieves the element's ElementType.

### insertText(offset Integer, text String)

Returns: Text

Inserts the specified text at the given character offset.

### isAtDocumentEnd()

Returns: Boolean

Determines whether the element is at the end of the Document.

### isBold()

Returns: Boolean | null

Retrieves the bold setting.

### isBold(offset Integer)

Returns: Boolean | null

Retrieves the bold setting at the specified character offset.

### isItalic()

Returns: Boolean | null

Retrieves the italic setting.

### isItalic(offset Integer)

Returns: Boolean | null

Retrieves the italic setting at the specified character offset.

### isStrikethrough()

Returns: Boolean | null

Retrieves the strikethrough setting.

### isStrikethrough(offset Integer)

Returns: Boolean | null

Retrieves the strikethrough setting at the specified character offset.

### isUnderline()

Returns: Boolean | null

Retrieves the underline setting.

### isUnderline(offset Integer)

Returns: Boolean | null

Retrieves the underline setting at the specified character offset.

### merge()

Returns: Text | null

Merges the element with the preceding sibling of the same type.

### removeFromParent()

Returns: Text | null

Removes the element from its parent.

### replaceText(searchPattern String, replacement String)

Returns: Element

Replaces all occurrences of a given text pattern with a given replacement string, using regular expressions.

### setAttributes(startOffset Integer, endOffsetInclusive Integer, attributes Object)

Returns: Text

Applies the specified attributes to the given character range.

### setAttributes(attributes Object)

Returns: Text

Sets the element's attributes.

### setBackgroundColor(startOffset Integer, endOffsetInclusive Integer, color String)

Returns: Text

Sets the background color for the specified character range.

### setBackgroundColor(color String)

Returns: Text

Sets the background color.

### setBold(bold Boolean)

Returns: Text

Sets the bold setting.

### setBold(startOffset Integer, endOffsetInclusive Integer, bold Boolean)

Returns: Text

Sets the bold setting for the specified character range.

### setFontFamily(startOffset Integer, endOffsetInclusive Integer, fontFamilyName String)

Returns: Text

Sets the font family for the specified character range.

### setFontFamily(fontFamilyName String)

Returns: Text

Sets the font family.

### setFontSize(startOffset Integer, endOffsetInclusive Integer, size Number)

Returns: Text

Sets the font size for the specified character range.

### setFontSize(size Number)

Returns: Text

Sets the font size.

### setForegroundColor(startOffset Integer, endOffsetInclusive Integer, color String)

Returns: Text

Sets the foreground color for the specified character range.

### setForegroundColor(color String)

Returns: Text

Sets the foreground color.

### setItalic(italic Boolean)

Returns: Text

Sets the italic setting.

### setItalic(startOffset Integer, endOffsetInclusive Integer, italic Boolean)

Returns: Text

Sets the italic setting for the specified character range.

### setLinkUrl(startOffset Integer, endOffsetInclusive Integer, url String)

Returns: Text

Sets the link URL for the specified character range.

### setLinkUrl(url String)

Returns: Text

Sets the link url.

### setStrikethrough(strikethrough Boolean)

Returns: Text

Sets the strikethrough setting.

### setStrikethrough(startOffset Integer, endOffsetInclusive Integer, strikethrough Boolean)

Returns: Text

Sets the strikethrough setting for the specified character range.

### setText(text String)

Returns: Text

Sets the text contents.

### setTextAlignment(startOffset Integer, endOffsetInclusive Integer, textAlignment TextAlignment)

Returns: Text

Sets the text alignment for a given character range.

### setTextAlignment(textAlignment TextAlignment)

Returns: Text

Sets the text alignment.

### setUnderline(underline Boolean)

Returns: Text

Sets the underline setting.

### setUnderline(startOffset Integer, endOffsetInclusive Integer, underline Boolean)

Returns: Text

Sets the underline setting for the specified character range.
