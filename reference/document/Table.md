# Table

An element representing a table.

A `Table` may only contain `TableRow` elements. When creating a `Table` that contains a large number of rows or cells, consider building it from a string array, as shown in the following example.

Scripts that use these methods require authorization with one or more of the following scopes: `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`.

## Methods

### appendTableRow()

Returns: TableRow

Creates and appends a new TableRow.

### appendTableRow(tableRow TableRow)

Returns: TableRow

Appends the given TableRow.

### clear()

Returns: Table

Clears the contents of the element.

### copy()

Returns: Table

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

### getBorderColor()

Returns: String | null

Retrieves the border color.

### getBorderWidth()

Returns: Number | null

Retrieves the border width, in points.

### getCell(rowIndex Integer, cellIndex Integer)

Returns: TableCell | null

Retrieves the TableCell at the specified row and cell indices.

### getChild(childIndex Integer)

Returns: Element

Retrieves the child element at the specified child index.

### getChildIndex(child Element)

Returns: Integer

Retrieves the child index for the specified child element.

### getColumnWidth(columnIndex Integer)

Returns: Number | null

Retrieves the width of the specified table column, in points.

### getLinkUrl()

Returns: String | null

Retrieves the link url.

### getNextSibling()

Returns: Element | null

Retrieves the element's next sibling element. The next sibling has the same parent and follows the current element.

### getNumChildren()

Returns: Integer

Retrieves the number of children.

### getNumRows()

Returns: Integer

Retrieves the number of TableRows.

### getParent()

Returns: ContainerElement | null

Retrieves the element's parent element.

### getPreviousSibling()

Returns: Element | null

Retrieves the element's previous sibling element.

### getRow(rowIndex Integer)

Returns: TableRow | null

Retrieves the TableRow at the specified row index.

### getText()

Returns: String

Retrieves the contents of the element as a text string.

### getTextAlignment()

Returns: TextAlignment | null

Gets the text alignment.

### getType()

Returns: ElementType

Retrieves the element's ElementType.

### insertTableRow(childIndex Integer)

Returns: TableRow

Creates and inserts a new TableRow at the specified index.

### insertTableRow(childIndex Integer, tableRow TableRow)

Returns: TableRow

Inserts the given TableRow at the specified index.

### isAtDocumentEnd()

Returns: Boolean

Determines whether the element is at the end of the Document.

### removeChild(child Element)

Returns: Table

Removes the specified child element.

### removeFromParent()

Returns: Table | null

Removes the element from its parent.

### removeRow(rowIndex Integer)

Returns: TableRow

Removes the TableRow at the specified row index.

### replaceText(searchPattern String, replacement String)

Returns: Element

Replaces all occurrences of a given text pattern with a given replacement string, using regular expressions.

### setAttributes(attributes Object)

Returns: Table

Sets the element's attributes.

### setBorderColor(color String)

Returns: Table

Sets the border color.

### setBorderWidth(width Number)

Returns: Table

Sets the border width, in points.

### setColumnWidth(columnIndex Integer, width Number)

Returns: Table

Sets the width of the specified column, in points.

### setLinkUrl(url String)

Returns: Table

Sets the link url.

### setTextAlignment(textAlignment TextAlignment)

Returns: Table

Sets the text alignment.
