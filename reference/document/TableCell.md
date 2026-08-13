# TableCell

An element representing a table cell.

A `TableCell` is always contained within a `TableRow` and may contain `ListItem`, `Paragraph`, or `Table` elements.

Scripts that use these methods require authorization with one or more of the following scopes: `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`.

## Example

```javascript
const body = DocumentApp.getActiveDocument().getActiveTab().asDocumentTab().getBody();

// Insert two paragraphs separated by a paragraph containing a horizontal rule.
body.insertParagraph(0, 'An editAsText sample.');
body.insertHorizontalRule(0);
body.insertParagraph(0, 'An example.');

// Delete " sample.\n\n An" removing the horizontal rule in the process.
body.editAsText().deleteText(14, 25);
```

## Methods

### appendHorizontalRule()

Returns: HorizontalRule

Creates and appends a new HorizontalRule. The HorizontalRule will be contained in a new Paragraph.

### appendImage(image BlobSource)

Returns: InlineImage

Creates and appends a new InlineImage from the specified image blob. The InlineImage will be contained in a new Paragraph.

### appendImage(image InlineImage)

Returns: InlineImage

Appends the given InlineImage. The InlineImage will be contained in a new Paragraph.

### appendListItem(listItem ListItem)

Returns: ListItem

Appends the given ListItem.

### appendListItem(text String)

Returns: ListItem

Creates and appends a new ListItem.

### appendParagraph(paragraph Paragraph)

Returns: Paragraph

Appends the given Paragraph.

### appendParagraph(text String)

Returns: Paragraph

Creates and appends a new Paragraph.

### appendTable()

Returns: Table

Creates and appends a new Table.

### appendTable(cells String[][])

Returns: Table

Appends a new Table containing the specified cells.

### appendTable(table Table)

Returns: Table

Appends the given Table.

### clear()

Returns: TableCell

Clears the contents of the element.

### copy()

Returns: TableCell

Returns a detached, deep copy of the current element. Any child elements present in the element are also copied.

### editAsText()

Returns: Text

Obtains a Text version of the current element, for editing. Use `editAsText` for manipulating content as rich text; ignores non-text elements.

### findElement(elementType ElementType)

Returns: RangeElement | null

Searches the contents of the element for a descendant of the specified type.

### findElement(elementType ElementType, from RangeElement)

Returns: RangeElement | null

Searches the contents of the element for a descendant of the specified type, starting from the specified RangeElement.

### findText(searchPattern String)

Returns: RangeElement | null

Searches the contents of the element for the specified text pattern using regular expressions.

### findText(searchPattern String, from RangeElement)

Returns: RangeElement | null

Searches the contents of the element for the specified text pattern, starting from a given search result.

### getAttributes()

Returns: Object

Retrieves the element's attributes.

### getBackgroundColor()

Returns: String | null

Retrieves the background color.

### getChild(childIndex Integer)

Returns: Element

Retrieves the child element at the specified child index.

### getChildIndex(child Element)

Returns: Integer

Retrieves the child index for the specified child element.

### getColSpan()

Returns: Integer

Retrieves the column span, which is the number of columns of table cells this cell spans.

### getLinkUrl()

Returns: String | null

Retrieves the link url.

### getNextSibling()

Returns: Element | null

Retrieves the element's next sibling element.

### getNumChildren()

Returns: Integer

Retrieves the number of children.

### getPaddingBottom()

Returns: Number | null

Retrieves the bottom padding, in points.

### getPaddingLeft()

Returns: Number | null

Retrieves the left padding, in points.

### getPaddingRight()

Returns: Number | null

Retrieves the right padding, in points.

### getPaddingTop()

Returns: Number | null

Retrieves the top padding, in points.

### getParent()

Returns: ContainerElement | null

Retrieves the element's parent element.

### getParentRow()

Returns: TableRow | null

Retrieves the TableRow containing the current TableCell.

### getParentTable()

Returns: Table | null

Retrieves the Table containing the current TableCell.

### getPreviousSibling()

Returns: Element | null

Retrieves the element's previous sibling element.

### getRowSpan()

Returns: Integer

Retrieves the row span, which is the number of rows of table cells this cell spans.

### getText()

Returns: String

Retrieves the contents of the element as a text string.

### getTextAlignment()

Returns: TextAlignment | null

Gets the text alignment.

### getType()

Returns: ElementType

Retrieves the element's ElementType.

### getVerticalAlignment()

Returns: VerticalAlignment | null

Retrieves the VerticalAlignment.

### getWidth()

Returns: Number | null

Retrieves the width of the column containing the cell, in points.

### insertHorizontalRule(childIndex Integer)

Returns: HorizontalRule

Creates and inserts a new HorizontalRule at the specified index.

### insertImage(childIndex Integer, image BlobSource)

Returns: InlineImage

Creates and inserts an InlineImage from the specified image blob, at the specified index.

### insertImage(childIndex Integer, image InlineImage)

Returns: InlineImage

Inserts the given InlineImage at the specified index.

### insertListItem(childIndex Integer, listItem ListItem)

Returns: ListItem

Inserts the given ListItem at the specified index.

### insertListItem(childIndex Integer, text String)

Returns: ListItem

Creates and inserts a new ListItem at the specified index.

### insertParagraph(childIndex Integer, paragraph Paragraph)

Returns: Paragraph

Inserts the given Paragraph at the specified index.

### insertParagraph(childIndex Integer, text String)

Returns: Paragraph

Creates and inserts a new Paragraph at the specified index.

### insertTable(childIndex Integer)

Returns: Table

Creates and inserts a new Table at the specified index.

### insertTable(childIndex Integer, cells String[][])

Returns: Table

Creates and inserts a new Table containing the specified cells, at the specified index.

### insertTable(childIndex Integer, table Table)

Returns: Table

Inserts the given Table at the specified index.

### isAtDocumentEnd()

Returns: Boolean

Determines whether the element is at the end of the Document.

### merge()

Returns: TableCell | null

Merges the element with the preceding sibling of the same type.

### removeChild(child Element)

Returns: TableCell

Removes the specified child element.

### removeFromParent()

Returns: TableCell | null

Removes the element from its parent.

### replaceText(searchPattern String, replacement String)

Returns: Element

Replaces all occurrences of a given text pattern with a given replacement string, using regular expressions.

### setAttributes(attributes Object)

Returns: TableCell

Sets the element's attributes.

### setBackgroundColor(color String)

Returns: TableCell

Sets the background color.

### setLinkUrl(url String)

Returns: TableCell

Sets the link url.

### setPaddingBottom(paddingBottom Number)

Returns: TableCell

Sets the bottom padding, in points.

### setPaddingLeft(paddingLeft Number)

Returns: TableCell

Sets the left padding, in points.

### setPaddingRight(paddingRight Number)

Returns: TableCell

Sets the right padding, in points.

### setPaddingTop(paddingTop Number)

Returns: TableCell

Sets the top padding, in points.

### setText(text String)

Returns: TableCell

Sets the contents as plain text.

### setTextAlignment(textAlignment TextAlignment)

Returns: TableCell

Sets the text alignment.

### setVerticalAlignment(alignment VerticalAlignment)

Returns: TableCell

Sets the vertical alignment.

### setWidth(width Number)

Returns: TableCell

Sets the width of the column containing the current cell, in points.
