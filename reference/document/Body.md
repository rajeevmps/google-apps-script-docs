# Body

The Body represents the content of a tab in a Google Docs document.

The Body represents the content of a tab in a Google Docs document. It may contain ListItem, Paragraph, Table, and TableOfContents elements. The Body typically contains the full tab's contents except for HeaderSection, FooterSection, and FootnoteSection elements.

Scripts using documented methods require authorization with either `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents` scopes.

## Methods

### appendHorizontalRule()

Returns: HorizontalRule

Creates and appends a new HorizontalRule. The HorizontalRule will be contained in a new Paragraph.

### appendImage(image)

Returns: InlineImage

Creates and appends a new InlineImage from the specified image blob. The image will be contained in a new Paragraph.

### appendImage(image)

Returns: InlineImage

Appends the given InlineImage. The InlineImage will be contained in a new Paragraph. Use this version of appendImage when appending a copy of an existing InlineImage.

### appendListItem(listItem)

Returns: ListItem

Appends the given ListItem. Use this version of appendListItem when appending a copy of an existing ListItem.

### appendListItem(text)

Returns: ListItem

Creates and appends a new ListItem containing the specified text contents. Consecutive list items are added as part of the same list.

### appendPageBreak()

Returns: PageBreak

Creates and appends a new PageBreak. The PageBreak will be contained in a new Paragraph.

### appendPageBreak(pageBreak)

Returns: PageBreak

Appends the given PageBreak. The PageBreak will be contained in a new Paragraph. Use this version when appending a copy of an existing PageBreak.

### appendParagraph(paragraph)

Returns: Paragraph

Appends the given Paragraph. Use this version of appendParagraph when appending a copy of an existing Paragraph.

### appendParagraph(text)

Returns: Paragraph

Creates and appends a new Paragraph containing the specified text contents.

### appendTable()

Returns: Table

Creates and appends a new Table. This method will also append an empty paragraph after the table.

### appendTable(cells)

Returns: Table

Appends a new Table containing a TableCell for each specified string value. This method will also append an empty paragraph after the table.

### appendTable(table)

Returns: Table

Appends the given Table. Use this version of appendTable when appending a copy of an existing Table. This method will also append an empty paragraph after the table.

### clear()

Returns: Body

Clears the contents of the element.

### copy()

Returns: Body

Returns a detached, deep copy of the current element. Any child elements present in the element are also copied. The new element doesn't have a parent.

### editAsText()

Returns: Text

Obtains a Text version of the current element, for editing. Use editAsText for manipulating the elements contents as rich text. The editAsText mode ignores non-text elements.

### findElement(elementType)

Returns: RangeElement|null

Searches the contents of the element for a descendant of the specified type.

### findElement(elementType, from)

Returns: RangeElement|null

Searches the contents of the element for a descendant of the specified type, starting from the specified RangeElement.

### findText(searchPattern)

Returns: RangeElement|null

Searches the contents of the element for the specified text pattern using regular expressions.

### findText(searchPattern, from)

Returns: RangeElement|null

Searches the contents of the element for the specified text pattern, starting from a given search result.

### getAttributes()

Returns: Object

Retrieves the element's attributes.

### getChild(childIndex)

Returns: Element

Retrieves the child element at the specified child index.

### getChildIndex(child)

Returns: Integer

Retrieves the child index for the specified child element.

### getHeadingAttributes(paragraphHeading)

Returns: Object

Retrieves the set of attributes for the provided ParagraphHeading.

### getImages()

Returns: InlineImage[]|null

Retrieves all the InlineImages contained in the section.

### getListItems()

Returns: ListItem[]|null

Retrieves all the ListItems contained in the section.

### getMarginBottom()

Returns: Number|null

Retrieves the bottom margin, in points.

### getMarginLeft()

Returns: Number|null

Retrieves the left margin, in points.

### getMarginRight()

Returns: Number|null

Retrieves the right margin.

### getMarginTop()

Returns: Number|null

Retrieves the top margin.

### getNumChildren()

Returns: Integer

Retrieves the number of children.

### getPageHeight()

Returns: Number|null

Retrieves the page height, in points.

### getPageWidth()

Returns: Number|null

Retrieves the page width, in points.

### getParagraphs()

Returns: Paragraph[]|null

Retrieves all the Paragraphs contained in the section (including ListItems).

### getParent()

Returns: ContainerElement|null

Retrieves the element's parent element.

### getTables()

Returns: Table[]|null

Retrieves all the Tables contained in the section.

### getText()

Returns: String

Retrieves the contents of the element as a text string.

### getTextAlignment()

Returns: TextAlignment|null

Gets the text alignment.

### getType()

Returns: ElementType

Retrieves the element's ElementType.

### insertHorizontalRule(childIndex)

Returns: HorizontalRule

Creates and inserts a new HorizontalRule at the specified index.

### insertImage(childIndex, image)

Returns: InlineImage

Creates and inserts an InlineImage from the specified image blob, at the specified index.

### insertImage(childIndex, image)

Returns: InlineImage

Inserts the given InlineImage at the specified index.

### insertListItem(childIndex, listItem)

Returns: ListItem

Inserts the given ListItem at the specified index.

### insertListItem(childIndex, text)

Returns: ListItem

Creates and inserts a new ListItem at the specified index, containing the specified text contents.

### insertPageBreak(childIndex)

Returns: PageBreak

Creates and inserts a new PageBreak at the specified index.

### insertPageBreak(childIndex, pageBreak)

Returns: PageBreak

Inserts the given PageBreak at the specified index.

### insertParagraph(childIndex, paragraph)

Returns: Paragraph

Inserts the given Paragraph at the specified index.

### insertParagraph(childIndex, text)

Returns: Paragraph

Creates and inserts a new Paragraph at the specified index, containing the specified text contents.

### insertTable(childIndex)

Returns: Table

Creates and inserts a new Table at the specified index.

### insertTable(childIndex, cells)

Returns: Table

Creates and inserts a new Table containing the specified cells, at the specified index.

### insertTable(childIndex, table)

Returns: Table

Inserts the given Table at the specified index.

### removeChild(child)

Returns: Body

Removes the specified child element.

### replaceText(searchPattern, replacement)

Returns: Element

Replaces all occurrences of a given text pattern with a given replacement string, using regular expressions.

### setAttributes(attributes)

Returns: Body

Sets the element's attributes.

### setHeadingAttributes(paragraphHeading, attributes)

Returns: Body

Sets the attributes for the provided ParagraphHeading.

### setMarginBottom(marginBottom)

Returns: Body

Sets the bottom margin, in points.

### setMarginLeft(marginLeft)

Returns: Body

Sets the left margin, in points.

### setMarginRight(marginRight)

Returns: Body

Sets the right margin, in points.

### setMarginTop(marginTop)

Returns: Body

Sets the top margin.

### setPageHeight(pageHeight)

Returns: Body

Sets the page height, in points.

### setPageWidth(pageWidth)

Returns: Body

Sets the page width, in points.

### setText(text)

Returns: Body

Sets the contents as plain text.

### setTextAlignment(textAlignment)

Returns: Body

Sets the text alignment.

## Deprecated Methods

### getFootnotes()

Returns: Footnote[]|null

Retrieves all the Footnotes contained in the section.

### getLinkUrl()

Returns: String|null

Retrieves the link url.

### getNextSibling()

Returns: Element|null

Retrieves the element's next sibling element.

### getPreviousSibling()

Returns: Element|null

Retrieves the element's previous sibling element.

### isAtDocumentEnd()

Returns: Boolean

Determines whether the element is at the end of the Document.

### setLinkUrl(url)

Returns: Body

Sets the link url.
