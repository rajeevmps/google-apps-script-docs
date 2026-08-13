# Element

A generic element.

A generic element. Document contents are represented as elements. For example, ListItem, Paragraph, and Table are elements and inherit all of the methods defined by Element, such as getType().

## Methods

| Method | Return Type | Brief Description |
|--------|-------------|-------------------|
| `asBody()` | `Body` | Returns the current element as a Body |
| `asDate()` | `Date` | Returns the current element as a Date |
| `asEquation()` | `Equation` | Returns the current element as an Equation |
| `asEquationFunction()` | `EquationFunction` | Returns the current element as an EquationFunction |
| `asEquationFunctionArgumentSeparator()` | `EquationFunctionArgumentSeparator` | Returns the current element as an EquationFunctionArgumentSeparator |
| `asEquationSymbol()` | `EquationSymbol` | Returns the current element as an EquationSymbol |
| `asFooterSection()` | `FooterSection` | Returns the current element as a FooterSection |
| `asFootnote()` | `Footnote` | Returns the current element as a Footnote |
| `asFootnoteSection()` | `FootnoteSection` | Returns the current element as a FootnoteSection |
| `asHeaderSection()` | `HeaderSection` | Returns the current element as a HeaderSection |
| `asHorizontalRule()` | `HorizontalRule` | Returns the current element as a HorizontalRule |
| `asInlineDrawing()` | `InlineDrawing` | Returns the current element as an InlineDrawing |
| `asInlineImage()` | `InlineImage` | Returns the current element as an InlineImage |
| `asListItem()` | `ListItem` | Returns the current element as a ListItem |
| `asPageBreak()` | `PageBreak` | Returns the current element as a PageBreak |
| `asParagraph()` | `Paragraph` | Returns the current element as a Paragraph |
| `asPerson()` | `Person` | Returns the current element as a Person |
| `asRichLink()` | `RichLink` | Returns the current element as a RichLink |
| `asTable()` | `Table` | Returns the current element as a Table |
| `asTableCell()` | `TableCell` | Returns the current element as a TableCell |
| `asTableOfContents()` | `TableOfContents` | Returns the current element as a TableOfContents |
| `asTableRow()` | `TableRow` | Returns the current element as a TableRow |
| `asText()` | `Text` | Returns the current element as a Text |
| `copy()` | `Element` | Returns a detached, deep copy of the current element |
| `getAttributes()` | `Object` | Retrieves the element's attributes |
| `getNextSibling()` | `Element\|null` | Retrieves the element's next sibling element |
| `getParent()` | `ContainerElement\|null` | Retrieves the element's parent element |
| `getPreviousSibling()` | `Element\|null` | Retrieves the element's previous sibling element |
| `getType()` | `ElementType` | Retrieves the element's ElementType |
| `isAtDocumentEnd()` | `Boolean` | Determines whether the element is at the end of the Document |
| `merge()` | `Element\|null` | Merges the element with the preceding sibling of the same type |
| `removeFromParent()` | `Element\|null` | Removes the element from its parent |
| `setAttributes(attributes)` | `Element` | Sets the element's attributes |

### asBody()

Returns: Body — The current element.

Returns the current element as a `Body`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asDate()

Returns: Date — The current element with its type set as Date.

Returns the current element as a `Date`. When you know an element is a `Date`, use this method to set its type as a `Date`. Doing so lets autocomplete in the Apps Script editor show you the methods you can use with a `Date`.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asEquation()

Returns: Equation — The current element.

Returns the current element as an `Equation`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asEquationFunction()

Returns: EquationFunction — The current element.

Returns the current element as a `EquationFunction`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asEquationFunctionArgumentSeparator()

Returns: EquationFunctionArgumentSeparator — The current element.

Returns the current element as a `EquationFunctionArgumentSeparator`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asEquationSymbol()

Returns: EquationSymbol — The current element.

Returns the current element as a `EquationSymbol`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asFooterSection()

Returns: FooterSection — The current element.

Returns the current element as a `FooterSection`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asFootnote()

Returns: Footnote — The current element.

Returns the current element as a `Footnote`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asFootnoteSection()

Returns: FootnoteSection — The current element.

Returns the current element as a `FootnoteSection`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asHeaderSection()

Returns: HeaderSection — The current element.

Returns the current element as a `HeaderSection`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asHorizontalRule()

Returns: HorizontalRule — The current element.

Returns the current element as a `HorizontalRule`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asInlineDrawing()

Returns: InlineDrawing — The current element.

Returns the current element as a `InlineDrawing`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asInlineImage()

Returns: InlineImage — The current element.

Returns the current element as a `InlineImage`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asListItem()

Returns: ListItem — The current element.

Returns the current element as a `ListItem`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asPageBreak()

Returns: PageBreak — The current element.

Returns the current element as a `PageBreak`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asParagraph()

Returns: Paragraph — The current element.

Returns the current element as a `Paragraph`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asPerson()

Returns: Person — The current element with its type set as Person.

Returns the current element as a `Person`. When you know an element is a `Person`, use this method to set its type as a person. Doing so lets autocomplete in the Apps Script editor show you the methods you can use with a person element.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asRichLink()

Returns: RichLink — The current element with its type set as RichLink.

Returns the current element as a `RichLink`, for example, a link to a Google Sheets file. When you know an element is a `RichLink`, use this method to set its type as a `RichLink`. Doing so lets autocomplete in the Apps Script editor show you the methods you can use with a `RichLink`.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asTable()

Returns: Table — The current element.

Returns the current element as a `Table`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asTableCell()

Returns: TableCell — The current element.

Returns the current element as a `TableCell`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asTableOfContents()

Returns: TableOfContents — The current element.

Returns the current element as a `TableOfContents`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asTableRow()

Returns: TableRow — The current element.

Returns the current element as a `TableRow`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asText()

Returns: Text — The current element.

Returns the current element as a `Text`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### copy()

Returns: Element — A copy of the element.

Returns a detached, deep copy of the current element.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getAttributes()

Returns: Object — The element's attributes.

Retrieves the element's attributes.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getNextSibling()

Returns: Element|null — The next sibling element.

Retrieves the element's next sibling element.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getParent()

Returns: ContainerElement|null — The parent element.

Retrieves the element's parent element.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getPreviousSibling()

Returns: Element|null — The previous sibling element.

Retrieves the element's previous sibling element.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getType()

Returns: ElementType — The element's type.

Retrieves the element's `ElementType`.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### isAtDocumentEnd()

Returns: Boolean — Whether the element is at document end.

Determines whether the element is at the end of the `Document`.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### merge()

Returns: Element|null — The merged element.

Merges the element with the preceding sibling of the same type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### removeFromParent()

Returns: Element|null — The removed element.

Removes the element from its parent.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### setAttributes(attributes)

Returns: Element — The current element.

Sets the element's attributes.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

## Properties

None.
