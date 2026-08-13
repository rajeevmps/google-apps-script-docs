# Text

A representation of an XML `Text` node.

A representation of an XML `Text` node.

## Methods

### append(text)

Returns: `Text`

Appends the given text to any content that already exists in the node.

**Parameters:**
- `text` (String) - The text to append to the node.

**Return:** `Text` - The `Text` node, for chaining.

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

Gets the text value of the `Text` node.

**Return:** `String` - The text value of the `Text` node.

### getValue()

Returns: `String`

Gets the text value of all nodes that are direct or indirect children of the node, in the order they appear.

**Return:** `String` - The text value of all nodes that are direct or indirect children.

### setText(text)

Returns: `Text`

Sets the text value of the `Text` node.

**Parameters:**
- `text` (String) - The text value to set.

**Return:** `Text` - The `Text` node, for chaining.

## Properties

None.

No code samples were provided on this reference page.
