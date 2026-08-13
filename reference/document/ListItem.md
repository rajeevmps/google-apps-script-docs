# ListItem

An element representing a list item.

An element representing a list item. A `ListItem` is a `Paragraph` that is associated with a list ID. A `ListItem` can contain `Equation`, `Footnote`, `HorizontalRule`, `InlineDrawing`, `InlineImage`, `PageBreak`, and `Text` elements. For more information on document structure, see the guide to extending Google Docs.

In the Google Docs UI, `ListItem` elements with the same list ID are part of the same list, and are numbered/ordered accordingly, regardless of the position of the elements within the document structure (i.e. items with the same list ID that are not necessarily siblings of one another or contained within the same parent element will be numbered as though they are part of the same, single list).

## Example

```javascript
const body = DocumentApp.getActiveDocument().getActiveTab().asDocumentTab().getBody();

const item1 = body.appendListItem('Item 1');
Logger.log(item1.getListId());

body.appendTable([['Cell 1', 'Cell 2']]);

const item2 = body.appendListItem('Item 2');
item2.setListId(item1);
```

## Methods

### addPositionedImage(image BlobSource)

Returns: PositionedImage

Creates and inserts a new `PositionedImage` from the specified image blob.

### appendHorizontalRule()

Returns: HorizontalRule

Creates and appends a new `HorizontalRule`.

### appendInlineImage(image BlobSource)

Returns: InlineImage

Creates and appends a new `InlineImage` from the specified image blob.

### appendInlineImage(image InlineImage)

Returns: InlineImage

Appends the given `InlineImage`.

### appendPageBreak()

Returns: PageBreak

Creates and appends a new `PageBreak`. Note: `PageBreaks` may not be contained within `TableCells`. If the current element is contained in a table cell, an exception will be thrown.

### appendPageBreak(pageBreak PageBreak)

Returns: PageBreak

Appends the given `PageBreak`. Note: `PageBreaks` may not be contained within `TableCells`. If the current element is contained in a table cell, an exception will be thrown.

### appendText(text String)

Returns: Text

Creates and appends a new `Text` element with the specified contents.

### appendText(text Text)

Returns: Text

Appends the given `Text` element.

### clear()

Returns: ListItem

Clears the contents of the element.

### copy()

Returns: ListItem

Returns a detached, deep copy of the current element. Any child elements present in the element are also copied. The new element doesn't have a parent.

### editAsText()

Returns: Text

Obtains a `Text` version of the current element, for editing. Use `editAsText` for manipulating the elements contents as rich text. The `editAsText` mode ignores non-text elements (such as `InlineImage` and `HorizontalRule`). Child elements fully contained within a deleted text range are removed from the element.

### findElement(elementType ElementType)

Returns: RangeElement|null

Searches the contents of the element for a descendant of the specified type.

### findElement(elementType ElementType, from RangeElement)

Returns: RangeElement|null

Searches the contents of the element for a descendant of the specified type, starting from the specified `RangeElement`.

### findText(searchPattern String)

Returns: RangeElement|null

Searches the contents of the element for the specified text pattern using regular expressions. A subset of the JavaScript regular expression features are not fully supported, such as capture groups and mode modifiers. The provided regular expression pattern is independently matched against each text block contained in the current element.

### findText(searchPattern String, from RangeElement)

Returns: RangeElement|null

Searches the contents of the element for the specified text pattern, starting from a given search result. A subset of the JavaScript regular expression features are not fully supported, such as capture groups and mode modifiers.

### getAlignment()

Returns: HorizontalAlignment|null

Retrieves the `HorizontalAlignment`.

### getAttributes()

Returns: Object

Retrieves the element's attributes.

### getChild(childIndex Integer)

Returns: Element

Retrieves the child element at the specified child index.

### getChildIndex(child Element)

Returns: Integer

Retrieves the child index for the specified child element.

### getGlyphType()

Returns: GlyphType|null

Retrieves the list item's `GlyphType`.

### getHeading()

Returns: ParagraphHeading|null

Retrieves the `ParagraphHeading`.

### getIndentEnd()

Returns: Number|null

Retrieves the end indentation, in points.

### getIndentFirstLine()

Returns: Number|null

Retrieves the first line indentation, in points.

### getIndentStart()

Returns: Number|null

Retrieves the start indentation.

### getLineSpacing()

Returns: Number|null

Retrieves the line spacing, in points.

### getLinkUrl()

Returns: String|null

Retrieves the link url.

### getListId()

Returns: String|null

Retrieves the list ID.

### getNestingLevel()

Returns: Integer

Retrieves the list item's nesting level.

### getNextSibling()

Returns: Element|null

Retrieves the element's next sibling element.

### getNumChildren()

Returns: Integer

Retrieves the number of children.

### getParent()

Returns: ContainerElement|null

Retrieves the element's parent element.

### getPositionedImage(id String)

Returns: PositionedImage

Gets a `PositionedImage` by the image's ID.

### getPositionedImages()

Returns: PositionedImage[]

Gets all `PositionedImage` objects anchored to the paragraph.

### getPreviousSibling()

Returns: Element|null

Retrieves the element's previous sibling element.

### getSpacingAfter()

Returns: Number|null

Retrieves the spacing after the element, in points.

### getSpacingBefore()

Returns: Number|null

Retrieves the spacing before the element, in points.

### getText()

Returns: String

Retrieves the contents of the element as a text string.

### getTextAlignment()

Returns: TextAlignment|null

Gets the text alignment.

### getType()

Returns: ElementType

Retrieves the element's `ElementType`.

### insertHorizontalRule(childIndex Integer)

Returns: HorizontalRule

Creates and inserts a `HorizontalRule` at the specified index.

### insertInlineImage(childIndex Integer, image BlobSource)

Returns: InlineImage

Creates and inserts a new `InlineImage` from the specified image blob, at the specified index.

### insertInlineImage(childIndex Integer, image InlineImage)

Returns: InlineImage

Inserts the given `InlineImage` at the specified index.

### insertPageBreak(childIndex Integer)

Returns: PageBreak

Creates and inserts a new `PageBreak` at the specified index.

### insertPageBreak(childIndex Integer, pageBreak PageBreak)

Returns: PageBreak

Inserts the given `PageBreak` at the specified index.

### insertText(childIndex Integer, text String)

Returns: Text

Creates and inserts a new text element at the specified index.

### insertText(childIndex Integer, text Text)

Returns: Text

Inserts the given `Text` element at the specified index, with the specified text contents.

### isAtDocumentEnd()

Returns: Boolean

Determines whether the element is at the end of the `Document`.

### isLeftToRight()

Returns: Boolean|null

Retrieves the left-to-right setting.

### merge()

Returns: ListItem|null

Merges the element with the preceding sibling of the same type.

### removeChild(child Element)

Returns: ListItem

Removes the specified child element.

### removeFromParent()

Returns: ListItem|null

Removes the element from its parent.

### removePositionedImage(id String)

Returns: Boolean

Removes a `PositionedImage` by the image's ID.

### replaceText(searchPattern String, replacement String)

Returns: Element

Replaces all occurrences of a given text pattern with a given replacement string, using regular expressions.

### setAlignment(alignment HorizontalAlignment)

Returns: ListItem

Sets the `HorizontalAlignment`.

### setAttributes(attributes Object)

Returns: ListItem

Sets the element's attributes.

### setGlyphType(glyphType GlyphType)

Returns: ListItem

Sets the list item's `GlyphType`.

### setHeading(heading ParagraphHeading)

Returns: ListItem

Sets the `ParagraphHeading`.

### setIndentEnd(indentEnd Number)

Returns: ListItem

Sets the end indentation, in points.

### setIndentFirstLine(indentFirstLine Number)

Returns: ListItem

Sets the first line indentation, in points.

### setIndentStart(indentStart Number)

Returns: ListItem

Sets the start indentation, in points.

### setLeftToRight(leftToRight Boolean)

Returns: ListItem

Sets the left-to-right setting.

### setLineSpacing(multiplier Number)

Returns: ListItem

Sets the line spacing, as a quantity indicating the number of lines to use for spacing.

### setLinkUrl(url String)

Returns: ListItem

Sets the link url.

### setListId(listItem ListItem)

Returns: ListItem

Sets the list ID.

### setNestingLevel(nestingLevel Integer)

Returns: ListItem

Sets the list item's nesting level.

### setSpacingAfter(spacingAfter Number)

Returns: ListItem

Sets the spacing after the element, in points.

### setSpacingBefore(spacingBefore Number)

Returns: ListItem

Sets the spacing before the element, in points.

### setText(text String)

Returns: void

Sets the contents of the list item as text.

### setTextAlignment(textAlignment TextAlignment)

Returns: ListItem

Sets the text alignment.
