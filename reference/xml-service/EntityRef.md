# EntityRef

A representation of an XML `EntityReference` node.

A representation of an XML `EntityReference` node.

## Methods

### detach()

Returns: `Content`

Detaches the node from its parent `Element` node. If the node does not have a parent, this method has no effect.

**Return:** `Content` - The detached node.

### getName()

Returns: `String`

Gets the name of the `EntityReference` node.

**Return:** `String` - The name of the `EntityReference` node.

### getParentElement()

Returns: `Element`

Gets the node's parent `Element` node. If the node does not have a parent, this method returns `null`.

**Return:** `Element` - The parent `Element` node.

### getPublicId()

Returns: `String`

Gets the public ID of the `EntityReference` node. If the node does not have a public ID, this method returns `null`.

**Return:** `String` - The public ID of the `EntityReference` node, or `null` if it has none.

### getSystemId()

Returns: `String`

Gets the system ID of the `EntityReference` node. If the node does not have a system ID, this method returns `null`.

**Return:** `String` - The system ID of the `EntityReference` node, or `null` if it has none.

### getValue()

Returns: `String`

Gets the text value of all nodes that are direct or indirect children of the node, in the order they appear in the document.

**Return:** `String` - The text value of all nodes that are direct or indirect children of the node.

### setName(name)

Returns: `EntityRef`

Sets the name of the `EntityReference` node.

**Parameters:**
- `name` (String) - The name to set.

**Return:** `EntityRef` - The `EntityReference` node, for chaining.

### setPublicId(id)

Returns: `EntityRef`

Sets the public ID of the `EntityReference` node.

**Parameters:**
- `id` (String) - The public ID to set.

**Return:** `EntityRef` - The `EntityReference` node, for chaining.

### setSystemId(id)

Returns: `EntityRef`

Sets the system ID of the `EntityReference` node.

**Parameters:**
- `id` (String) - The system ID to set.

**Return:** `EntityRef` - The `EntityReference` node, for chaining.

## Properties

None.

No code samples were provided on this reference page.
