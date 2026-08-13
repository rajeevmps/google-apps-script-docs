# ProcessingInstruction

A representation of an XML `ProcessingInstruction` node.

A representation of an XML `ProcessingInstruction` node.

## Methods

### detach()

Returns: `Content`

Detaches the node from its parent `Element` node. If the node does not have a parent, this method has no effect.

**Return:** `Content` - The detached node.

### getData()

Returns: `String`

Gets the raw data for every instruction in the `ProcessingInstruction` node.

**Return:** `String` - The raw data for every instruction in the `ProcessingInstruction` node.

### getParentElement()

Returns: `Element`

Gets the node's parent `Element` node. If the node does not have a parent, this method returns `null`.

**Return:** `Element` - The parent `Element` node.

### getTarget()

Returns: `String`

Gets the target for the `ProcessingInstruction` node.

**Return:** `String` - The target for the `ProcessingInstruction` node.

### getValue()

Returns: `String`

Gets the text value of all nodes that are direct or indirect children of the node, in the order they appear in the document.

**Return:** `String` - The text value of all nodes that are direct or indirect children of the node.

## Properties

None.

No code samples were provided on this reference page.
