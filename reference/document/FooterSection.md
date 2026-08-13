# FooterSection

An element representing a footer section.

An element representing a footer section. A `Document` typically contains at most one `FooterSection`. The `FooterSection` may contain `ListItem`, `Paragraph`, and `Table` elements.

## Example

```javascript
const body =
    DocumentApp.getActiveDocument().getActiveTab().asDocumentTab().getBody();

// Insert two paragraphs separated by a paragraph containing an
// horizontal rule.
body.insertParagraph(0, 'An editAsText sample.');
body.insertHorizontalRule(0);
body.insertParagraph(0, 'An example.');

// Delete " sample.\n\n An" removing the horizontal rule in the process.
body.editAsText().deleteText(14, 25);
```

## Methods

| Method | Return Type | Brief Description |
|--------|-------------|-------------------|
| `appendHorizontalRule()` | `HorizontalRule` | Creates and appends a new `HorizontalRule`. |
| `appendImage(image)` | `InlineImage` | Creates and appends a new `InlineImage` from the specified image blob. |
| `appendImage(image)` | `InlineImage` | Appends the given `InlineImage`. |
| `appendListItem(listItem)` | `ListItem` | Appends the given `ListItem`. |
| `appendListItem(text)` | `ListItem` | Creates and appends a new `ListItem` containing the specified text contents. |
| `appendParagraph(paragraph)` | `Paragraph` | Appends the given `Paragraph`. |
| `appendParagraph(text)` | `Paragraph` | Creates and appends a new `Paragraph` containing the specified text contents. |
| `appendTable()` | `Table` | Creates and appends a new `Table`. |
| `appendTable(cells)` | `Table` | Appends a new `Table` containing a `TableCell` for each specified string value. |
| `appendTable(table)` | `Table` | Appends the given `Table`. |
| `clear()` | `FooterSection` | Clears the contents of the element. |
| `copy()` | `FooterSection` | Returns a detached, deep copy of the current element. |
| `editAsText()` | `Text` | Obtains a `Text` version of the current element, for editing. |
| `findElement(elementType)` | `RangeElement\|null` | Searches the contents of the element for a descendant of the specified type. |
| `findElement(elementType, from)` | `RangeElement\|null` | Searches the contents of the element for a descendant of the specified type, starting from the specified `RangeElement`. |
| `findText(searchPattern)` | `RangeElement\|null` | Searches the contents of the element for the specified text pattern using regular expressions. |
| `findText(searchPattern, from)` | `RangeElement\|null` | Searches the contents of the element for the specified text pattern, starting from a given search result. |
| `getAttributes()` | `Object` | Retrieves the element's attributes. |
| `getChild(childIndex)` | `Element` | Retrieves the child element at the specified child index. |
| `getChildIndex(child)` | `Integer` | Retrieves the child index for the specified child element. |
| `getImages()` | `InlineImage[]\|null` | Retrieves all the `InlineImages` contained in the section. |
| `getListItems()` | `ListItem[]\|null` | Retrieves all the `ListItems` contained in the section. |
| `getNumChildren()` | `Integer` | Retrieves the number of children. |
| `getParagraphs()` | `Paragraph[]\|null` | Retrieves all the `Paragraphs` contained in the section (including `ListItems`). |
| `getParent()` | `ContainerElement\|null` | Retrieves the element's parent element. |
| `getTables()` | `Table[]\|null` | Retrieves all the `Tables` contained in the section. |
| `getText()` | `String` | Retrieves the contents of the element as a text string. |
| `getTextAlignment()` | `TextAlignment\|null` | Gets the text alignment. |
| `getType()` | `ElementType` | Retrieves the element's `ElementType`. |
| `insertHorizontalRule(childIndex)` | `HorizontalRule` | Creates and inserts a new `HorizontalRule` at the specified index. |
| `insertImage(childIndex, image)` | `InlineImage` | Creates and inserts an `InlineImage` from the specified image blob, at the specified index. |
| `insertImage(childIndex, image)` | `InlineImage` | Inserts the given `InlineImage` at the specified index. |
| `insertListItem(childIndex, listItem)` | `ListItem` | Inserts the given `ListItem` at the specified index. |
| `insertListItem(childIndex, text)` | `ListItem` | Creates and inserts a new `ListItem` at the specified index, containing the specified text contents. |
| `insertParagraph(childIndex, paragraph)` | `Paragraph` | Inserts the given `Paragraph` at the specified index. |
| `insertParagraph(childIndex, text)` | `Paragraph` | Creates and inserts a new `Paragraph` at the specified index, containing the specified text contents. |
| `insertTable(childIndex)` | `Table` | Creates and inserts a new `Table` at the specified index. |
| `insertTable(childIndex, cells)` | `Table` | Creates and inserts a new `Table` containing the specified cells, at the specified index. |
| `insertTable(childIndex, table)` | `Table` | Inserts the given `Table` at the specified index. |
| `removeChild(child)` | `FooterSection` | Removes the specified child element. |
| `removeFromParent()` | `FooterSection\|null` | Removes the element from its parent. |
| `replaceText(searchPattern, replacement)` | `Element` | Replaces all occurrences of a given text pattern with a given replacement string, using regular expressions. |
| `setAttributes(attributes)` | `FooterSection` | Sets the element's attributes. |
| `setText(text)` | `FooterSection` | Sets the contents as plain text. |
| `setTextAlignment(textAlignment)` | `FooterSection` | Sets the text alignment. |

### Deprecated methods

| Method | Return Type | Brief Description |
|--------|-------------|-------------------|
| `getFootnotes()` | `Footnote[]\|null` | Retrieves all the `Footnotes` contained in the section. |
| `getLinkUrl()` | `String\|null` | Retrieves the link url. |
| `getNextSibling()` | `Element` | Retrieves the element's next sibling element. |
| `getPreviousSibling()` | `Element` | Retrieves the element's previous sibling element. |
| `isAtDocumentEnd()` | `Boolean` | Determines whether the element is at the end of the `Document`. |
| `setLinkUrl(url)` | `FooterSection` | Sets the link url. |

### appendHorizontalRule()

Returns: HorizontalRule

Creates and appends a new `HorizontalRule`. The `HorizontalRule` will be contained in a new `Paragraph`.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### appendImage(image: BlobSource)

Returns: InlineImage

Creates and appends a new `InlineImage` from the specified image blob. The image will be contained in a new `Paragraph`.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### appendImage(image: InlineImage)

Returns: InlineImage

Appends the given `InlineImage`. The `InlineImage` will be contained in a new `Paragraph`. Use this version of `appendImage` when appending a copy of an existing `InlineImage`.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### appendListItem(listItem: ListItem)

Returns: ListItem

Appends the given `ListItem`. Use this version of `appendListItem` when appending a copy of an existing `ListItem`.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### appendListItem(text: String)

Returns: ListItem

Creates and appends a new `ListItem` containing the specified text contents. Consecutive list items are added as part of the same list.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### appendParagraph(paragraph: Paragraph)

Returns: Paragraph

Appends the given `Paragraph`. Use this version of `appendParagraph` when appending a copy of an existing `Paragraph`.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### appendParagraph(text: String)

Returns: Paragraph

Creates and appends a new `Paragraph` containing the specified text contents.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### appendTable()

Returns: Table

Creates and appends a new `Table`. This method will also append an empty paragraph after the table, since Google Docs documents cannot end with a table.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### appendTable(cells: String[][])

Returns: Table

Appends a new `Table` containing a `TableCell` for each specified string value. This method will also append an empty paragraph after the table, since Google Docs documents cannot end with a table.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### appendTable(table: Table)

Returns: Table

Appends the given `Table`. Use this version of `appendTable` when appending a copy of an existing `Table`. This method will also append an empty paragraph after the table, since Google Docs documents cannot end with a table.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### clear()

Returns: FooterSection

Clears the contents of the element.

### copy()

Returns: FooterSection

Returns a detached, deep copy of the current element. Any child elements present in the element are also copied. The new element doesn't have a parent.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### editAsText()

Returns: Text

Obtains a `Text` version of the current element, for editing. Use `editAsText` for manipulating the elements contents as rich text. The `editAsText` mode ignores non-text elements (such as `InlineImage` and `HorizontalRule`). Child elements fully contained within a deleted text range are removed from the element.

```javascript
const body =
    DocumentApp.getActiveDocument().getActiveTab().asDocumentTab().getBody();

// Insert two paragraphs separated by a paragraph containing an
// horizontal rule.
body.insertParagraph(0, 'An editAsText sample.');
body.insertHorizontalRule(0);
body.insertParagraph(0, 'An example.');

// Delete " sample.\n\n An" removing the horizontal rule in the process.
body.editAsText().deleteText(14, 25);
```

### findElement(elementType: ElementType)

Returns: RangeElement|null

Searches the contents of the element for a descendant of the specified type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### findElement(elementType: ElementType, from: RangeElement)

Returns: RangeElement|null

Searches the contents of the element for a descendant of the specified type, starting from the specified `RangeElement`.

```javascript
const body =
    DocumentApp.getActiveDocument().getActiveTab().asDocumentTab().getBody();

// Define the search parameters.
let searchResult = null;

// Search until the paragraph is found.
while (
    (searchResult = body.findElement(
         DocumentApp.ElementType.PARAGRAPH,
         searchResult,
         ))) {
  const par = searchResult.getElement().asParagraph();
  if (par.getHeading() === DocumentApp.ParagraphHeading.HEADING1) {
    // Found one, update and stop.
    par.setText('This is the first header.');
    break;
  }
}
```

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### findText(searchPattern: String)

Returns: RangeElement|null

Searches the contents of the element for the specified text pattern using regular expressions. A subset of the JavaScript regular expression features are not fully supported, such as capture groups and mode modifiers. The provided regular expression pattern is independently matched against each text block contained in the current element.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### findText(searchPattern: String, from: RangeElement)

Returns: RangeElement|null

Searches the contents of the element for the specified text pattern, starting from a given search result. A subset of the JavaScript regular expression features are not fully supported, such as capture groups and mode modifiers. The provided regular expression pattern is independently matched against each text block contained in the current element.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getAttributes()

Returns: Object

Retrieves the element's attributes.

### getChild(childIndex: Integer)

Returns: Element

Retrieves the child element at the specified child index.

### getChildIndex(child: Element)

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

### insertHorizontalRule(childIndex: Integer)

Returns: HorizontalRule

Creates and inserts a new `HorizontalRule` at the specified index.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### insertImage(childIndex: Integer, image: BlobSource)

Returns: InlineImage

Creates and inserts an `InlineImage` from the specified image blob, at the specified index.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### insertImage(childIndex: Integer, image: InlineImage)

Returns: InlineImage

Inserts the given `InlineImage` at the specified index.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### insertListItem(childIndex: Integer, listItem: ListItem)

Returns: ListItem

Inserts the given `ListItem` at the specified index.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### insertListItem(childIndex: Integer, text: String)

Returns: ListItem

Creates and inserts a new `ListItem` at the specified index, containing the specified text contents.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### insertParagraph(childIndex: Integer, paragraph: Paragraph)

Returns: Paragraph

Inserts the given `Paragraph` at the specified index.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### insertParagraph(childIndex: Integer, text: String)

Returns: Paragraph

Creates and inserts a new `Paragraph` at the specified index, containing the specified text contents.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### insertTable(childIndex: Integer)

Returns: Table

Creates and inserts a new `Table` at the specified index.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### insertTable(childIndex: Integer, cells: String[][])

Returns: Table

Creates and inserts a new `Table` containing the specified cells, at the specified index.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### insertTable(childIndex: Integer, table: Table)

Returns: Table

Inserts the given `Table` at the specified index.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### removeChild(child: Element)

Returns: FooterSection

Removes the specified child element.

### removeFromParent()

Returns: FooterSection|null

Removes the element from its parent.

### replaceText(searchPattern: String, replacement: String)

Returns: Element

Replaces all occurrences of a given text pattern with a given replacement string, using regular expressions.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### setAttributes(attributes: Object)

Returns: FooterSection

Sets the element's attributes.

### setText(text: String)

Returns: FooterSection

Sets the contents as plain text.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### setTextAlignment(textAlignment: TextAlignment)

Returns: FooterSection

Sets the text alignment.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getFootnotes() (Deprecated)

Returns: Footnote[]|null

Retrieves all the `Footnotes` contained in the section.

### getLinkUrl() (Deprecated)

Returns: String|null

Retrieves the link url.

### getNextSibling() (Deprecated)

Returns: Element

Retrieves the element's next sibling element.

### getPreviousSibling() (Deprecated)

Returns: Element

Retrieves the element's previous sibling element.

### isAtDocumentEnd() (Deprecated)

Returns: Boolean

Determines whether the element is at the end of the `Document`.

### setLinkUrl(url: String) (Deprecated)

Returns: FooterSection

Sets the link url.

## Properties

None.
