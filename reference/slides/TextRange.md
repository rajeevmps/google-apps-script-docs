# TextRange

A segment of the text contents of a Shape or a TableCell.

A segment of the text contents of a Shape or a TableCell.

If you use methods that edit how the text fits within a shape, any autofit settings applied to the shape are deactivated.

## Methods

### appendParagraph(text)

`Paragraph`

Appends a paragraph at the end of the text range. The paragraph maintains the styling of the end of the current text range.

The provided text string is appended as a paragraph by adding at least one surrounding newline character to the string.

When the provided text string contains newline characters (thus consisting of multiple paragraphs), the final paragraph added is returned.

**Parameters**

- `text` (`String`) — The string to append as a paragraph.

**Returns**

`Paragraph` — The appended Paragraph.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### appendRange(textRange)

`TextRange`

Appends a copy of the provided text range to the end of the current text range.

The formatting of the inserted text matches that of the source text.

**Parameters**

- `textRange` (`TextRange`) — The text range to append.

**Returns**

`TextRange` — The text range representing the appended text.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### appendRange(textRange, matchSourceFormatting)

`TextRange`

Appends a copy of the provided text range to the end of the current text range.

If set to match the formatting of the destination text, AutoText within the provided text range are replaced with their rendered values. Furthermore, any non-text elements within the provided text range are not appended.

**Parameters**

- `textRange` (`TextRange`) — The text range to append.
- `matchSourceFormatting` (`Boolean`) — If true, match the formatting of the source text; if false, match the formatting of the destination text.

**Returns**

`TextRange` — The text range representing the appended text.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### appendText(text)

`TextRange`

Appends text at the end of the text range. The text maintains the styling of the end of the existing text.

**Parameters**

- `text` (`String`) — The string to append.

**Returns**

`TextRange` — The text range representing the appended text.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### asRenderedString()

`String`

Returns the rendered text bounded by this range of the associated shape or table cell in a format appropriate to display to end users.

AutoText elements, such as generated slide numbers, are replaced with their rendered values. Any non-text elements in the range are omitted.

**Returns**

`String` — The rendered text in the range.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### asString()

`String`

Returns the raw text bounded by this range of the associated shape or table cell.

AutoText elements such as generated slide numbers and any non-text elements in the range are replaced with the Unicode character U+E907.

**Returns**

`String` — The raw text in the range.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### clear()

Clears the text bounded by this range.

Since the entire text in a Shape or TableCell must end in a newline, the final newline in the text is not removed.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### clear(startOffset, endOffset)

Clears the text bounded by the start and end offsets in the range.

Since the text must end in a newline, the final newline in text is not removed even if it's covered by the given offsets.

**Parameters**

- `startOffset` (`Integer`) — The number of characters past the start index of the current text range used to determine the inclusive start index of the range to clear. The start offset must be equal to or greater than 0 and less than or equal to endOffset. startOffset must also be less than the length of the current range.
- `endOffset` (`Integer`) — The number of characters past the start index of the current text range used to determine the exclusive end index of the range to clear. The endOffset must be equal to or greater than startOffset. endOffset must also be less than or equal to the length of the current range.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### find(pattern)

`TextRange[]`

Returns all the ranges matching the search pattern in the current text range. The search is case sensitive.

**Parameters**

- `pattern` (`String`) — The regular expression pattern to search; any backslashes in the pattern should be escaped.

**Returns**

`TextRange[]` — A list of text ranges.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### find(pattern, startOffset)

`TextRange[]`

Returns all the ranges matching the search pattern in the current text range starting from the start offset. The search is case sensitive.

**Parameters**

- `pattern` (`String`) — The regular expression pattern to search; any backslashes in the pattern should be escaped.
- `startOffset` (`Integer`) — The number of characters past the start index of the current text range used to determine the inclusive start index of the range to search. startOffset must also be less than the length of the current range.

**Returns**

`TextRange[]` — A list of text ranges.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getAutoTexts()

`AutoText[]`

Returns the auto texts within the current text range.

**Returns**

`AutoText[]` — A list of auto texts.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getEndIndex()

`Integer`

Returns the exclusive, 0-based index for the last character in this range. If the start and end indices are equal, the range is considered to be empty.

**Returns**

`Integer` — The end index of the range.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getLength()

`Integer`

Returns the number of characters in this range.

**Returns**

`Integer` — The number of characters in this range.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getLinks()

`TextRange[]`

Returns a collection of text ranges that correspond to all Links within the current text range or overlapping the current text range.

Each returned range is guaranteed to span one link when it is created. Text modifications can cause it to no longer represent exactly one link.

Each Link on the returned ranges can be accessed via TextStyle.getLink().

```javascript
// Accesses the first link on a TextRange object.
const textRange = SlidesApp.getActivePresentation().getSlides()[0].getShapes()[0].getText();
const linkTextRange = textRange.getLinks()[0];
const textStyle = linkTextRange.getTextStyle();
Logger.log(textStyle.hasLink());   // logs 'true'
const link = textStyle.getLink();  // Link object
```

**Returns**

`TextRange[]` — A list of text ranges.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getListParagraphs()

`Paragraph[]`

Returns the paragraphs in lists that overlap the current text range.

**Returns**

`Paragraph[]` — A list of paragraphs in lists.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getListStyle()

`ListStyle`

Returns the ListStyle of the current text range.

**Returns**

`ListStyle` — The list style of the current text range.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getParagraphStyle()

`ParagraphStyle`

Returns the ParagraphStyle of the current text range.

**Returns**

`ParagraphStyle` — The paragraph style of the current text range.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getParagraphs()

`Paragraph[]`

Returns the paragraphs that overlap the current text range.

**Returns**

`Paragraph[]` — A list of paragraphs.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getRange(startOffset, endOffset)

`TextRange`

Returns a new TextRange covering part of the range from which it is derived.

**Parameters**

- `startOffset` (`Integer`) — The number of characters past the start index of the current text range used to determine the inclusive start index of the returned range. The start offset must be equal to or greater than 0 and less than or equal to endOffset. startOffset must also be less than the length of the current range.
- `endOffset` (`Integer`) — The number of characters past the start index of the current text range used to determine the exclusive end index of the returned range. The endOffset must be equal to or greater than startOffset. endOffset must also be less than or equal to the length of the current range.

**Returns**

`TextRange` — A new text range.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getRuns()

`TextRange[]`

Returns the text runs that overlap the current text range. A text run is a segment of text where all the characters have the same text style.

Each returned range is only guaranteed to span one run when it is created. Text or style modifications can cause it to no longer represent exactly one run.

**Returns**

`TextRange[]` — A list of text ranges.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getStartIndex()

`Integer`

Returns the inclusive, 0-based index for the first character in this range. If the start and end indices are equal, the range is considered to be empty.

**Returns**

`Integer` — The start index of the range.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getTextStyle()

`TextStyle|null`

Returns the text style of the range, or null if the range is empty.

**Returns**

`TextStyle|null` — The text style of the range.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertParagraph(startOffset, text)

`Paragraph`

Inserts a paragraph at the start offset. The paragraph maintains the styling of the current text range at the start offset.

The provided text string is inserted as a paragraph by adding at least one surrounding newline character to the string.

When the provided text string contains newline characters (thus consisting of multiple paragraphs), the final paragraph added is returned.

**Parameters**

- `startOffset` (`Integer`) — The number of characters past the start index of the current text range used to determine the inclusive start index of the text to insert.
- `text` (`String`) — The string to insert.

**Returns**

`Paragraph` — The inserted Paragraph.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertRange(startOffset, textRange)

`TextRange`

Inserts a copy of the provided text range at the start offset.

The formatting of the inserted text matches that of the source text.

**Parameters**

- `startOffset` (`Integer`) — The number of characters past the start index of the current text range used to determine the inclusive start index of the text to insert.
- `textRange` (`TextRange`) — The text range to insert.

**Returns**

`TextRange` — The text range representing the inserted text.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertRange(startOffset, textRange, matchSourceFormatting)

`TextRange`

Inserts a copy of the provided text range at the start offset.

If set to match the formatting of the destination text, AutoText within the provided text range are replaced with their rendered values. Furthermore, any non-text elements within the provided text range are not inserted.

**Parameters**

- `startOffset` (`Integer`) — The number of characters past the start index of the current text range used to determine the inclusive start index of the text to insert.
- `textRange` (`TextRange`) — The text range to insert.
- `matchSourceFormatting` (`Boolean`) — If true, match the formatting of the source text; if false, match the formatting of the destination text.

**Returns**

`TextRange` — The text range representing the inserted text.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertText(startOffset, text)

`TextRange`

Inserts text at the start offset. The text maintains the styling of the existing text at the start offset.

**Parameters**

- `startOffset` (`Integer`) — The number of characters past the start index of the current text range used to determine the inclusive start index of the text to insert.
- `text` (`String`) — The string to insert.

**Returns**

`TextRange` — The text range representing the inserted text.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### isEmpty()

`Boolean`

Returns true if there are no characters in this range, and returns false otherwise.

**Returns**

`Boolean` — true if there are no characters in this range, and returns false otherwise.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### replaceAllText(findText, replaceText)

`Integer`

Replaces all instances of text matching find text with replace text. The search is case insensitive.

**Parameters**

- `findText` (`String`) — The text to find.
- `replaceText` (`String`) — The text to replace the matched text.

**Returns**

`Integer` — The number of occurrences changed.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### replaceAllText(findText, replaceText, matchCase)

`Integer`

Replaces all instances of text matching find text with replace text.

**Parameters**

- `findText` (`String`) — The text to find.
- `replaceText` (`String`) — The text to replace the matched text.
- `matchCase` (`Boolean`) — If true, the search is case sensitive; if false, the search is case insensitive.

**Returns**

`Integer` — The number of occurrences changed.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### select()

Selects only the TextRange in the active presentation and removes any previous selection.

A script can only access the selection of the user who is running the script, and only if the script is bound to the presentation.

The parent Page of the corresponding Shape or the TableCell is set as the current page selection. The Shape or the TableCell is set as the selected page element.

Selection

- 1. Range of text, use select on a non-empty TextRange to select the range of the characters.
- 2. Cursor position, use an empty TextRange to place the cursor at the desired index. const shape = SlidesApp.getActivePresentation().getSlides()[0].getShapes()[0]; shape.getText().setText('Hello'); // Range selection: Select the text range "He". shape.getText().getRange(0, 2).select(); // Cursor selection: Place the cursor after "H" like "H|ello". shape.getText().getRange(1, 1).select(); Authorization Scripts that use this method require authorization with one or more of the following scopes: https://www.googleapis.com/auth/presentations.currentonly https://www.googleapis.com/auth/presentations

### setText(newText)

`TextRange`

Sets the text bounded by this range of the associated shape or table cell. The text maintains the styling of the start of the existing text.

**Parameters**

- `newText` (`String`) — The string to set as the new text.

**Returns**

`TextRange` — The text range representing the set text.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

## Properties

This class has no properties listed on the reference page.
