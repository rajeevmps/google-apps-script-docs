# EquationSymbol

An element representing a symbol within a mathematical Equation.

An element representing a symbol within a mathematical `Equation`. An `EquationSymbol` cannot contain any other element. The `EquationSymbol` class provides methods to copy, get attributes, retrieve code, navigate siblings, get the parent element, check if it's at the document end, merge with a preceding sibling, remove from its parent, and set attributes.

## Methods

| Method | Return Type | Brief Description |
|--------|------------|-------------------|
| `copy()` | `EquationSymbol` | Returns a detached, deep copy of the current element. |
| `getAttributes()` | `Object` | Retrieves the element's attributes. |
| `getCode()` | `String` | Retrieves the code corresponding to the equation symbol. |
| `getNextSibling()` | `Element\|null` | Retrieves the element's next sibling element. |
| `getParent()` | `ContainerElement\|null` | Retrieves the element's parent element. |
| `getPreviousSibling()` | `Element\|null` | Retrieves the element's previous sibling element. |
| `getType()` | `ElementType` | Retrieves the element's ElementType. |
| `isAtDocumentEnd()` | `Boolean` | Determines whether the element is at the end of the Document. |
| `merge()` | `EquationSymbol\|null` | Merges the element with the preceding sibling of the same type. |
| `removeFromParent()` | `EquationSymbol\|null` | Removes the element from its parent. |
| `setAttributes(attributes)` | `EquationSymbol` | Sets the element's attributes. |

### copy()

Returns: EquationSymbol

Returns a detached, deep copy of the current element. Any child elements present in the element are also copied. The new element doesn't have a parent.

### getAttributes()

Returns: Object

Retrieves the element's attributes. The result is an object containing a property for each valid element attribute where each property name corresponds to an item in the `DocumentApp.Attribute` enumeration.

### getCode()

Returns: String

Retrieves the code corresponding to the equation symbol.

### getNextSibling()

Returns: Element|null

Retrieves the element's next sibling element. The next sibling has the same parent and follows the current element.

### getParent()

Returns: ContainerElement|null

Retrieves the element's parent element. The parent element contains the current element.

### getPreviousSibling()

Returns: Element|null

Retrieves the element's previous sibling element. The previous sibling has the same parent and precedes the current element.

### getType()

Returns: ElementType

Retrieves the element's `ElementType`. Use `getType()` to determine the exact type of a given element.

### isAtDocumentEnd()

Returns: Boolean

Determines whether the element is at the end of the `Document`.

### merge()

Returns: EquationSymbol|null

Merges the element with the preceding sibling of the same type. Only elements of the same `ElementType` can be merged. Any child elements contained in the current element are moved to the preceding sibling element. The current element is removed from the document.

### removeFromParent()

Returns: EquationSymbol|null

Removes the element from its parent.

### setAttributes(attributes)

Returns: EquationSymbol

Sets the element's attributes. The specified attributes parameter must be an object where each property name is an item in the `DocumentApp.Attribute` enumeration and each property value is the new value to be applied.

Parameters:
- `attributes` (`Object`)

## Properties

None.
