# HeaderSection

An element representing a header section.

An element representing a header section. A `Document` typically contains at most one `HeaderSection`. The `HeaderSection` may contain `ListItem`, `Paragraph`, and `Table` elements.

## Example

```javascript
const body = DocumentApp.getActiveDocument().getActiveTab().asDocumentTab().getBody();

// Insert two paragraphs separated by a paragraph containing a
// horizontal rule.
body.insertParagraph(0, 'An editAsText sample.');
body.insertHorizontalRule(0);
body.insertParagraph(0, 'An example.');

// Delete " sample.\n\n An" removing the horizontal rule in the process.
body.editAsText().deleteText(14, 25);
```

## Methods

### appendHorizontalRule()

Returns: HorizontalRule

Creates and appends a new `HorizontalRule`. The `HorizontalRule` will be contained in a new `Paragraph`.

### appendImage(image BlobSource)

Returns: InlineImage

Creates and appends a new `InlineImage` from the specified image blob. The image will be contained in a new `Paragraph`.

### appendImage(image InlineImage)

Returns: InlineImage

Appends the given `InlineImage`. The `InlineImage` will be contained in a new `Paragraph`. Use this version when appending a copy of an existing `InlineImage`.

### appendListItem(listItem ListItem)

Returns: ListItem

Appends the given `ListItem`. Use this version when appending a copy of an existing `ListItem`.

### appendListItem(text String)

Returns: ListItem

Creates and appends a new `ListItem` containing the specified text contents. Consecutive list items are added as part of the same list.

### appendParagraph(paragraph Paragraph)

Returns: Paragraph

Appends the given `Paragraph`. Use this version when appending a copy of an existing `Paragraph`.

### appendParagraph(text String)

Returns: Paragraph

Creates and appends a new `Paragraph` containing the specified text contents.

### appendTable()

Returns: Table

Creates and appends a new `Table`. This method will also append an empty paragraph after the table, since Google Docs documents cannot end with a table.

### appendTable(cells String[][])

Returns: Table

Appends a new `Table` containing a `TableCell` for each specified string value. This method will also append an empty paragraph after the table.

### appendTable(table Table)

Returns: Table

Appends the given `Table`. Use this version when appending a copy of an existing `Table`. This method will also append an empty paragraph after the table.

### insertHorizontalRule(childIndex Integer)

Returns: HorizontalRule

Creates and inserts a new `HorizontalRule` at the specified index.

### insertImage(childIndex Integer, image BlobSource)

Returns: InlineImage

Creates and inserts an `InlineImage` from the specified image blob, at the specified index.

### insertImage(childIndex Integer, image InlineImage)

Returns: InlineImage

Inserts the given `InlineImage` at the specified index.

### insertListItem(childIndex Integer, listItem ListItem)

Returns: ListItem

Inserts the given `ListItem` at the specified index.

### insertListItem(childIndex Integer, text String)

Returns: ListItem

Creates and inserts a new `ListItem` at the specified index, containing the specified text contents.

### insertParagraph(childIndex Integer, paragraph Paragraph)

Returns: Paragraph

Inserts the given `Paragraph` at the specified index.

### insertParagraph(childIndex Integer, text String)

Returns: Paragraph

Creates and inserts a new `Paragraph` at the specified index, containing the specified text contents.

### insertTable(childIndex Integer)

Returns: Table

Creates and inserts a new `Table` at the specified index.

### insertTable(childIndex Integer, cells String[][])

Returns: Table

Creates and inserts a new `Table` containing the specified cells, at the specified index.

### insertTable(childIndex Integer, table Table)

Returns: Table

Inserts the given `Table` at the specified index.

### clear()

Returns: HeaderSection

Clears the contents of the element.

### copy()

Returns: HeaderSection

Returns a detached, deep copy of the current element. Any child elements present are also copied. The new element doesn't have a parent.

### editAsText()

Returns: Text

Obtains a `Text` version of the current element, for editing. Use `editAsText` for manipulating elements as rich text. The mode ignores non-text elements. Child elements fully contained within deleted text ranges are removed.

### replaceText(searchPattern String, replacement String)

Returns: Element

Replaces all occurrences of a given text pattern with a given replacement string, using regular expressions.

### setText(text String)

Returns: HeaderSection

Sets the contents as plain text.

### findElement(elementType ElementType)

Returns: RangeElement|null

Searches the contents of the element for a descendant of the specified type.

### findElement(elementType ElementType, from RangeElement)

Returns: RangeElement|null

Searches the contents of the element for a descendant of the specified type, starting from the specified `RangeElement`.

### findText(searchPattern String)

Returns: RangeElement|null

Searches the contents for the specified text pattern using regular expressions. A subset of JavaScript regex features are not fully supported. The pattern is matched against each text block independently.

### findText(searchPattern String, from RangeElement)

Returns: RangeElement|null

Searches the contents for the specified text pattern, starting from a given search result. A subset of JavaScript regex features are not fully supported.

### getAttributes()

Returns: Object

Retrieves the element's attributes.

### getChild(childIndex Integer)

Returns: Element

Retrieves the child element at the specified child index.

### getChildIndex(child Element)

Returns: Integer

Retrieves the child index for the specified child element.

### getImages()

Returns: InlineImage[]|null

Retrieves all the `InlineImages` contained in the section.

### getListItems()

Returns: ListItem[]|null

Retrieves all the `ListItems` contained in the section.

### getNumChildren()

Returns: Integer

Retrieves the number of children.

### getParagraphs()

Returns: Paragraph[]|null

Retrieves all the `Paragraphs` contained in the section (including `ListItems`).

### getParent()

Returns: ContainerElement|null

Retrieves the element's parent element.

### getTables()

Returns: Table[]|null

Retrieves all the `Tables` contained in the section.

### getText()

Returns: String

Retrieves the contents of the element as a text string.

### getTextAlignment()

Returns: TextAlignment|null

Gets the text alignment.

### getType()

Returns: ElementType

Retrieves the element's `ElementType`.

### setAttributes(attributes Object)

Returns: HeaderSection

Sets the element's attributes.

### setTextAlignment(textAlignment TextAlignment)

Returns: HeaderSection

Sets the text alignment.

### removeChild(child Element)

Returns: HeaderSection

Removes the specified child element.

### removeFromParent()

Returns: HeaderSection|null

Removes the element from its parent.

## Deprecated Methods

### getFootnotes()

Returns: Footnote[]|null

Deprecated.

### getLinkUrl()

Returns: String|null

Deprecated.

### getNextSibling()

Returns: Element

Deprecated.

### getPreviousSibling()

Returns: Element

Deprecated.

### isAtDocumentEnd()

Returns: Boolean

Deprecated.

### setLinkUrl(url String)

Returns: HeaderSection

Deprecated.
