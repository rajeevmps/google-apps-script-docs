# DocType

A representation of an XML `DocumentType` node.

A representation of an XML `DocumentType` node. The DocType class provides methods to manage XML DocumentType nodes, including getting and setting element names, internal/external subset data, and parent element relationships.

## Methods

### detach()

Returns: `Content`

Detaches the node from its parent `Element` node. If the node does not have a parent, this method has no effect.

**Return:** `Content` - The detached node.

### getElementName()

Returns: `String`

Gets the name of the root `Element` node specified in the `DocType` declaration.

**Return:** `String` - The name of the root `Element` node specified in the `DocType` declaration.

### getInternalSubset()

Returns: `String`

Gets the internal subset data for the `DocumentType` node.

**Return:** `String` - The internal subset data.

### getParentElement()

Returns: `Element`

Gets the node's parent `Element` node. If the node does not have a parent, this method returns `null`.

**Return:** `Element` - The parent `Element` node.

### getPublicId()

Returns: `String`

Gets the public ID of the external subset data for the `DocumentType` node.

**Return:** `String` - The public ID of the external subset data.

### getSystemId()

Returns: `String`

Gets the system ID of the external subset data for the `DocumentType` node.

**Return:** `String` - The system ID of the external subset data.

### getValue()

Returns: `String`

Gets the text value of all nodes that are direct or indirect children of the node, in the order they appear in the document.

**Return:** `String` - The text value of all nodes that are direct or indirect children of the node.

### setElementName(name)

Returns: `DocType`

Sets the name of the root `Element` node to specify in the `DocType` declaration.

**Parameters:**
- `name` (String) - The name of the root `Element` node to specify in the `DocType` declaration.

**Return:** `DocType` - The `DocumentType` node, for chaining.

### setInternalSubset(data)

Returns: `DocType`

Sets the internal subset data for the `DocumentType` node.

**Parameters:**
- `data` (String) - The internal subset data to set.

**Return:** `DocType` - The `DocumentType` node, for chaining.

### setPublicId(id)

Returns: `DocType`

Sets the public ID of the external subset data for the `DocumentType` node.

**Parameters:**
- `id` (String) - The public ID of the external subset data to set.

**Return:** `DocType` - The `DocumentType` node, for chaining.

### setSystemId(id)

Returns: `DocType`

Sets the system ID of the external subset data for the `DocumentType` node.

**Parameters:**
- `id` (String) - The system ID of the external subset data to set.

**Return:** `DocType` - The `DocumentType` node, for chaining.

## Properties

None.

No code samples were provided on this reference page.
