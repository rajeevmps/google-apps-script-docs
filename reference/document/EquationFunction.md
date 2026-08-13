# EquationFunction

An element representing a function in a mathematical Equation.

An element representing a function in a mathematical `Equation`. An `EquationFunction` may contain `EquationFunction`, `EquationFunctionArgumentSeparator`, `EquationSymbol`, and `Text` elements.

## Methods

| Method | Return Type | Brief Description |
|--------|-------------|-------------------|
| `clear()` | `EquationFunction` | Clears the contents of the element. |
| `copy()` | `EquationFunction` | Returns a detached, deep copy of the current element. |
| `editAsText()` | `Text` | Obtains a `Text` version of the current element, for editing. |
| `findElement(elementType)` | `RangeElement\|null` | Searches the contents of the element for a descendant of the specified type. |
| `findElement(elementType, from)` | `RangeElement\|null` | Searches the contents of the element for a descendant of the specified type, starting from the specified `RangeElement`. |
| `findText(searchPattern)` | `RangeElement\|null` | Searches the contents of the element for the specified text pattern using regular expressions. |
| `findText(searchPattern, from)` | `RangeElement\|null` | Searches the contents of the element for the specified text pattern, starting from a given search result. |
| `getAttributes()` | `Object` | Retrieves the element's attributes. |
| `getChild(childIndex)` | `Element` | Retrieves the child element at the specified child index. |
| `getChildIndex(child)` | `Integer` | Retrieves the child index for the specified child element. |
| `getCode()` | `String` | Retrieves the code corresponding to the equation function. |
| `getLinkUrl()` | `String\|null` | Retrieves the link url. |
| `getNextSibling()` | `Element\|null` | Retrieves the element's next sibling element. |
| `getNumChildren()` | `Integer` | Retrieves the number of children. |
| `getParent()` | `ContainerElement\|null` | Retrieves the element's parent element. |
| `getPreviousSibling()` | `Element\|null` | Retrieves the element's previous sibling element. |
| `getText()` | `String` | Retrieves the contents of the element as a text string. |
| `getTextAlignment()` | `TextAlignment\|null` | Gets the text alignment. |
| `getType()` | `ElementType` | Retrieves the element's `ElementType`. |
| `isAtDocumentEnd()` | `Boolean` | Determines whether the element is at the end of the `Document`. |
| `merge()` | `EquationFunction\|null` | Merges the element with the preceding sibling of the same type. |
| `removeFromParent()` | `EquationFunction\|null` | Removes the element from its parent. |
| `replaceText(searchPattern, replacement)` | `Element` | Replaces all occurrences of a given text pattern with a given replacement string. |
| `setAttributes(attributes)` | `EquationFunction` | Sets the element's attributes. |
| `setLinkUrl(url)` | `EquationFunction` | Sets the link url. |
| `setTextAlignment(textAlignment)` | `EquationFunction` | Sets the text alignment. |

### clear()

Returns: EquationFunction — The current element.

Clears the contents of the element.

### copy()

Returns: EquationFunction

Returns a detached, deep copy of the current element. Any child elements present in the element are also copied. The new element doesn't have a parent.

### editAsText()

Returns: Text

Obtains a `Text` version of the current element, for editing. Use `editAsText` for manipulating the elements contents as rich text. The `editAsText` mode ignores non-text elements (such as `InlineImage` and `HorizontalRule`). Child elements fully contained within a deleted text range are removed from the element.

### findElement(elementType)

Returns: RangeElement|null

Searches the contents of the element for a descendant of the specified type.

Parameters:
- `elementType` (`ElementType`)

### findElement(elementType, from)

Returns: RangeElement|null

Searches the contents of the element for a descendant of the specified type, starting from the specified `RangeElement`.

Parameters:
- `elementType` (`ElementType`)
- `from` (`RangeElement`)

### findText(searchPattern)

Returns: RangeElement|null

Searches the contents of the element for the specified text pattern using regular expressions. A subset of the JavaScript regular expression features are not fully supported, such as capture groups and mode modifiers. The provided regular expression pattern is independently matched against each text block contained in the current element.

Parameters:
- `searchPattern` (`String`)

### findText(searchPattern, from)

Returns: RangeElement|null

Searches the contents of the element for the specified text pattern, starting from a given search result. A subset of the JavaScript regular expression features are not fully supported, such as capture groups and mode modifiers. The provided regular expression pattern is independently matched against each text block contained in the current element.

Parameters:
- `searchPattern` (`String`)
- `from` (`RangeElement`)

### getAttributes()

Returns: Object

Retrieves the element's attributes. The result is an object containing a property for each valid element attribute where each property name corresponds to an item in the `DocumentApp.Attribute` enumeration.

### getChild(childIndex)

Returns: Element

Retrieves the child element at the specified child index.

Parameters:
- `childIndex` (`Integer`)

### getChildIndex(child)

Returns: Integer

Retrieves the child index for the specified child element.

Parameters:
- `child` (`Element`)

### getCode()

Returns: String

Retrieves the code corresponding to the equation function.

### getLinkUrl()

Returns: String|null — the link URL, or null if the element contains multiple values for this attribute

Retrieves the link url.

### getNextSibling()

Returns: Element|null

Retrieves the element's next sibling element. The next sibling has the same parent and follows the current element.

### getNumChildren()

Returns: Integer

Retrieves the number of children.

### getParent()

Returns: ContainerElement|null

Retrieves the element's parent element. The parent element contains the current element.

### getPreviousSibling()

Returns: Element|null

Retrieves the element's previous sibling element. The previous sibling has the same parent and precedes the current element.

### getText()

Returns: String

Retrieves the contents of the element as a text string.

### getTextAlignment()

Returns: TextAlignment|null — the type of text alignment, or null if the text contains multiple types of text alignments or if text alignment has never been set

Gets the text alignment. The available types of alignment are `DocumentApp.TextAlignment.NORMAL`, `DocumentApp.TextAlignment.SUBSCRIPT`, and `DocumentApp.TextAlignment.SUPERSCRIPT`.

### getType()

Returns: ElementType

Retrieves the element's `ElementType`. Use `getType()` to determine the exact type of a given element.

### isAtDocumentEnd()

Returns: Boolean

Determines whether the element is at the end of the `Document`.

### merge()

Returns: EquationFunction|null

Merges the element with the preceding sibling of the same type. Only elements of the same `ElementType` can be merged. Any child elements contained in the current element are moved to the preceding sibling element. The current element is removed from the document.

### removeFromParent()

Returns: EquationFunction|null

Removes the element from its parent.

### replaceText(searchPattern, replacement)

Returns: Element

Replaces all occurrences of a given text pattern with a given replacement string, using regular expressions. The search pattern is passed as a string, not a JavaScript regular expression object. This methods uses Google's RE2 regular expression library, which limits the supported syntax. The provided regular expression pattern is independently matched against each text block contained in the current element.

Parameters:
- `searchPattern` (`String`)
- `replacement` (`String`)

### setAttributes(attributes)

Returns: EquationFunction

Sets the element's attributes. The specified attributes parameter must be an object where each property name is an item in the `DocumentApp.Attribute` enumeration and each property value is the new value to be applied.

Parameters:
- `attributes` (`Object`)

### setLinkUrl(url)

Returns: EquationFunction

Sets the link url.

Parameters:
- `url` (`String`)

### setTextAlignment(textAlignment)

Returns: EquationFunction

Sets the text alignment.

Parameters:
- `textAlignment` (`TextAlignment`)

## Properties

None.
