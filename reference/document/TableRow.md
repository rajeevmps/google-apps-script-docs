# TableRow

An element representing a table row.

A `TableRow` is always contained within a `Table` and may only contain `TableCell` elements.

Scripts that use these methods require authorization with one or more of the following scopes: `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`.

## Methods

### appendTableCell()

Returns: TableCell

Creates and appends a new TableCell.

### appendTableCell(textContents String)

Returns: TableCell

Appends the given TableCell containing the specified text.

### appendTableCell(tableCell TableCell)

Returns: TableCell

Appends the given TableCell.

### clear()

Returns: TableRow

Clears the contents of the element.

### copy()

Returns: TableRow

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

Searches the contents of the element for the specified text pattern, starting from a given search result. A subset of the JavaScript regular expression features are not fully supported, such as capture groups and mode modifiers. The provided regular expression pattern is independently matched against each text block contained in the current element.

### getAttributes()

Returns: Object

Retrieves the element's attributes. The result is an object containing a property for each valid element attribute where each property name corresponds to an item in the `DocumentApp.Attribute` enumeration.

### getCell(cellIndex Integer)

Returns: TableCell | null

Retrieves the TableCell at the specified cell index.

### getChild(childIndex Integer)

Returns: Element

Retrieves the child element at the specified child index.

### getChildIndex(child Element)

Returns: Integer

Retrieves the child index for the specified child element.

### getLinkUrl()

Returns: String | null

Retrieves the link url.

### getMinimumHeight()

Returns: Number | null

Retrieves the minimum height, in points.

### getNextSibling()

Returns: Element | null

Retrieves the element's next sibling element. The next sibling has the same parent and follows the current element.

### getNumCells()

Returns: Integer

Retrieves the number of cells in the row.

### getNumChildren()

Returns: Integer

Retrieves the number of children.

### getParent()

Returns: ContainerElement | null

Retrieves the element's parent element. The parent element contains the current element.

### getParentTable()

Returns: Table | null

Retrieves the Table containing the current row.

### getPreviousSibling()

Returns: Element | null

Retrieves the element's previous sibling element. The previous sibling has the same parent and precedes the current element.

### getText()

Returns: String

Retrieves the contents of the element as a text string.

### getTextAlignment()

Returns: TextAlignment | null

Gets the text alignment. The available types of alignment are `DocumentApp.TextAlignment.NORMAL`, `DocumentApp.TextAlignment.SUBSCRIPT`, and `DocumentApp.TextAlignment.SUPERSCRIPT`.

### getType()

Returns: ElementType

Retrieves the element's ElementType. Use `getType()` to determine the exact type of a given element.

### insertTableCell(childIndex Integer)

Returns: TableCell

Creates and inserts a new TableCell at the specified index.

### insertTableCell(childIndex Integer, textContents String)

Returns: TableCell

Inserts the given TableCell at the specified index, containing the given text.

### insertTableCell(childIndex Integer, tableCell TableCell)

Returns: TableCell

Inserts the given TableCell at the specified index.

### isAtDocumentEnd()

Returns: Boolean

Determines whether the element is at the end of the Document.

### merge()

Returns: TableRow | null

Merges the element with the preceding sibling of the same type.

### removeCell(cellIndex Integer)

Returns: TableCell

Removes the TableCell at the specified cell index.

### removeChild(child Element)

Returns: TableRow

Removes the specified child element.

### removeFromParent()

Returns: TableRow | null

Removes the element from its parent.

### replaceText(searchPattern String, replacement String)

Returns: Element

Replaces all occurrences of a given text pattern with a given replacement string, using regular expressions.

### setAttributes(attributes Object)

Returns: TableRow

Sets the element's attributes.

### setLinkUrl(url String)

Returns: TableRow

Sets the link url.

### setMinimumHeight(minHeight Number)

Returns: TableRow

Sets the minimum height, in points.

### setTextAlignment(textAlignment TextAlignment)

Returns: TableRow

Sets the text alignment.
