# Comment

A representation of an XML `Comment` node.

A representation of an XML `Comment` node. Methods enable detaching the Comment node, accessing its parent element, and getting or setting text values.

## Methods

### detach()

Returns: `Content`

Detaches the node from its parent `Element` node. If the node does not have a parent, this method has no effect.

**Return:** `Content` - The detached node.

### getParentElement()

Returns: `Element`

Gets the node's parent `Element` node. If the node does not have a parent, this method returns `null`.

**Return:** `Element` - The parent `Element` node.

### getText()

Returns: `String`

Gets the text value of the `Comment` node.

**Return:** `String` - The text value of the `Comment` node.

### getValue()

Returns: `String`

Gets the text value of all nodes that are direct or indirect children of the node, in the order they appear in the document.

**Return:** `String` - The text value of all nodes that are direct or indirect children of the node.

### setText(text)

Returns: `Comment`

Sets the text value of the `Comment` node.

**Parameters:**
- `text` (String) - The text value to set.

**Return:** `Comment` - The `Comment` node, for chaining.

## Properties

None.
