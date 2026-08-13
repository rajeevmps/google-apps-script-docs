# Paragraph

An element representing a paragraph.

A `Paragraph` may contain `Equation`, `Footnote`, `HorizontalRule`, `InlineDrawing`, `InlineImage`, `PageBreak`, and `Text` elements.

Paragraphs may not contain new-line characters. New-line characters ("\n") are converted to line-break characters ("\r").

Scripts that use these methods require authorization with one or more of the following scopes: `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`.

## Methods

### addPositionedImage(image BlobSource)

Returns: PositionedImage

Creates and inserts a new PositionedImage from the specified image blob.

### appendHorizontalRule()

Returns: HorizontalRule

Creates and appends a new HorizontalRule.

### appendInlineImage(image BlobSource)

Returns: InlineImage

Creates and appends a new InlineImage from the specified image blob.

### appendInlineImage(image InlineImage)

Returns: InlineImage

Appends the given InlineImage.

### appendPageBreak()

Returns: PageBreak

Creates and appends a new PageBreak. Note: PageBreaks may not be contained within TableCells; if the current element is contained in a table cell, an exception is thrown.

### appendPageBreak(pageBreak PageBreak)

Returns: PageBreak

Appends the given PageBreak.

### appendText(text String)

Returns: Text

Creates and appends a new Text element with the specified contents.

### appendText(text Text)

Returns: Text

Appends the given Text element.

### clear()

Returns: Paragraph

Clears the contents of the element.

### copy()

Returns: Paragraph

Returns a detached, deep copy of the current element. Any child elements present in the element are also copied. The new element doesn't have a parent.

### editAsText()

Returns: Text

Obtains a Text version of the current element, for editing. Use `editAsText` for manipulating the elements contents as rich text. The `editAsText` mode ignores non-text elements (such as InlineImage and HorizontalRule). Child elements fully contained within a deleted text range are removed from the element.

### findElement(elementType ElementType)

Returns: RangeElement | null

Searches the contents of the element for a descendant of the specified type.

### findElement(elementType ElementType, from RangeElement)

Returns: RangeElement | null

Searches the contents of the element for a descendant of the specified type, starting from the specified RangeElement.

### findText(searchPattern String)

Returns: RangeElement | null

Searches the contents of the element for the specified text pattern using regular expressions. A subset of the JavaScript regular expression features are not fully supported, such as capture groups and mode modifiers. The provided regular expression pattern is independently matched against each text block contained in the current element.

### findText(searchPattern String, from RangeElement)

Returns: RangeElement | null

Searches the contents of the element for the specified text pattern, starting from a given search result.

### getAlignment()

Returns: HorizontalAlignment | null

Retrieves the HorizontalAlignment.

### getAttributes()

Returns: Object

Retrieves the element's attributes. The result is an object containing a property for each valid element attribute where each property name corresponds to an item in the `DocumentApp.Attribute` enumeration.

### getChild(childIndex Integer)

Returns: Element

Retrieves the child element at the specified child index.

### getChildIndex(child Element)

Returns: Integer

Retrieves the child index for the specified child element.

### getHeading()

Returns: ParagraphHeading | null

Retrieves the ParagraphHeading.

### getIndentEnd()

Returns: Number | null

Retrieves the end indentation, in points.

### getIndentFirstLine()

Returns: Number | null

Retrieves the first line indentation, in points.

### getIndentStart()

Returns: Number | null

Retrieves the start indentation.

### getLineSpacing()

Returns: Number | null

Retrieves the line spacing, in points.

### getLinkUrl()

Returns: String | null

Retrieves the link url.

### getNextSibling()

Returns: Element | null

Retrieves the element's next sibling element. The next sibling has the same parent and follows the current element.

### getNumChildren()

Returns: Integer

Retrieves the number of children.

### getParent()

Returns: ContainerElement | null

Retrieves the element's parent element. The parent element contains the current element.

### getPositionedImage(id String)

Returns: PositionedImage

Gets a PositionedImage by the image's ID.

### getPositionedImages()

Returns: PositionedImage[]

Gets all PositionedImage objects anchored to the paragraph.

### getPreviousSibling()

Returns: Element | null

Retrieves the element's previous sibling element. The previous sibling has the same parent and precedes the current element.

### getSpacingAfter()

Returns: Number | null

Retrieves the spacing after the element, in points.

### getSpacingBefore()

Returns: Number | null

Retrieves the spacing before the element, in points.

### getText()

Returns: String

Retrieves the contents of the element as a text string.

### getTextAlignment()

Returns: TextAlignment | null

Gets the text alignment. The available types of alignment are `DocumentApp.TextAlignment.NORMAL`, `DocumentApp.TextAlignment.SUBSCRIPT`, and `DocumentApp.TextAlignment.SUPERSCRIPT`.

### getType()

Returns: ElementType

Retrieves the element's ElementType. Use `getType()` to determine the exact type of a given element.

### insertHorizontalRule(childIndex Integer)

Returns: HorizontalRule

Creates and inserts a HorizontalRule at the specified index.

### insertInlineImage(childIndex Integer, image BlobSource)

Returns: InlineImage

Creates and inserts a new InlineImage from the specified image blob, at the specified index.

### insertInlineImage(childIndex Integer, image InlineImage)

Returns: InlineImage

Inserts the given InlineImage at the specified index.

### insertPageBreak(childIndex Integer)

Returns: PageBreak

Creates and inserts a new PageBreak at the specified index.

### insertPageBreak(childIndex Integer, pageBreak PageBreak)

Returns: PageBreak

Inserts the given PageBreak at the specified index.

### insertText(childIndex Integer, text String)

Returns: Text

Creates and inserts a new text element at the specified index.

### insertText(childIndex Integer, text Text)

Returns: Text

Inserts the given Text element at the specified index, with the specified text contents.

### isAtDocumentEnd()

Returns: Boolean

Determines whether the element is at the end of the Document.

### isLeftToRight()

Returns: Boolean | null

Retrieves the left-to-right setting.

### merge()

Returns: Paragraph | null

Merges the element with the preceding sibling of the same type. Only elements of the same ElementType can be merged. Any child elements contained in the current element are moved to the preceding sibling element. The current element is removed from the document.

### removeChild(child Element)

Returns: Paragraph

Removes the specified child element.

### removeFromParent()

Returns: Paragraph | null

Removes the element from its parent.

### removePositionedImage(id String)

Returns: Boolean

Removes a PositionedImage by the image's ID.

### replaceText(searchPattern String, replacement String)

Returns: Element

Replaces all occurrences of a given text pattern with a given replacement string, using regular expressions. The search pattern is passed as a string, not a JavaScript regular expression object. Because of this you'll need to escape any backslashes in the pattern. This method uses Google's RE2 regular expression library, which limits the supported syntax.

### setAlignment(alignment HorizontalAlignment)

Returns: Paragraph

Sets the HorizontalAlignment.

### setAttributes(attributes Object)

Returns: Paragraph

Sets the element's attributes. The specified attributes parameter must be an object where each property name is an item in the `DocumentApp.Attribute` enumeration and each property value is the new value to be applied.

### setHeading(heading ParagraphHeading)

Returns: Paragraph

Sets the ParagraphHeading.

### setIndentEnd(indentEnd Number)

Returns: Paragraph

Sets the end indentation, in points.

### setIndentFirstLine(indentFirstLine Number)

Returns: Paragraph

Sets the first line indentation, in points.

### setIndentStart(indentStart Number)

Returns: Paragraph

Sets the start indentation, in points.

### setLeftToRight(leftToRight Boolean)

Returns: Paragraph

Sets the left-to-right setting.

### setLineSpacing(multiplier Number)

Returns: Paragraph

Sets the line spacing, as a quantity indicating the number of lines to use for spacing.

### setLinkUrl(url String)

Returns: Paragraph

Sets the link url.

### setSpacingAfter(spacingAfter Number)

Returns: Paragraph

Sets the spacing after the element, in points.

### setSpacingBefore(spacingBefore Number)

Returns: Paragraph

Sets the spacing before the element, in points.

### setText(text String)

Returns: void

Sets the contents of the paragraph as text.

### setTextAlignment(textAlignment TextAlignment)

Returns: Paragraph

Sets the text alignment. The available types of alignment are `DocumentApp.TextAlignment.NORMAL`, `DocumentApp.TextAlignment.SUBSCRIPT`, and `DocumentApp.TextAlignment.SUPERSCRIPT`.
