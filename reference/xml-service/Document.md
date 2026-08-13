# Document

A representation of an XML document.

A representation of an XML document. It includes methods for adding, getting, removing, and cloning content nodes that are immediate children or descendants of the document. The Document object allows for managing the root element and Document Type declaration. Methods are available to check for the presence of a root element and determine the number of immediate child nodes.

## Methods

### addContent(content)

Returns: `Document`

Appends the given node to the end of the document. The content argument can be a Content object or any node object that corresponds to a type listed in ContentTypes. Note, however, that a document can only have one child Element node, which is implicitly the root Element node.

**Parameters:**
- `content` (Content) - The node to append.

**Return:** `Document` - The document, for chaining.

### addContent(index, content)

Returns: `Document`

Inserts the given node at the given index among all nodes that are immediate children of the document. The content argument can be a Content object or any node object that corresponds to a type listed in ContentTypes. Note, however, that a document can only have one child Element node, which is implicitly the root Element node.

**Parameters:**
- `index` (Integer) - The index at which to insert the node among immediate children.
- `content` (Content) - The node to insert.

**Return:** `Document` - The document, for chaining.

### cloneContent()

Returns: `Content[]`

Creates unattached copies of all nodes that are immediate children of the document.

**Return:** `Content[]` - An array of unattached copies of all immediate child nodes.

### detachRootElement()

Returns: `Element`

Detaches and returns the document's root Element node. If the document does not have a root Element node, this method returns null.

**Return:** `Element` - The former root `Element` node.

### getAllContent()

Returns: `Content[]`

Gets all nodes that are immediate children of the document.

**Return:** `Content[]` - An array of all immediate child nodes.

### getContent(index)

Returns: `Content`

Gets the node at the given index among all nodes that are immediate children of the document. If there is no node at the given index, this method returns null.

**Parameters:**
- `index` (Integer) - The index for the node among immediate children.

**Return:** `Content` - The node, or `null` if none exists at that index.

### getContentSize()

Returns: `Integer`

Gets the number of nodes that are immediate children of the document.

**Return:** `Integer` - The count of immediate child nodes.

### getDescendants()

Returns: `Content[]`

Gets all nodes that are direct or indirect children of the document, in the order they appear in the document.

**Return:** `Content[]` - An array of all descendant nodes.

### getDocType()

Returns: `DocType`

Gets the document's DocType declaration. If the document does not have a DocumentType node, this method returns null.

**Return:** `DocType` - The document's DocType declaration.

### getRootElement()

Returns: `Element`

Gets the document's root Element node. If the document does not have a root Element node, this method returns null.

**Return:** `Element` - The document's root `Element` node.

### hasRootElement()

Returns: `Boolean`

Determines whether the document has a root Element node.

**Return:** `Boolean` - `true` if the document has a root `Element` node; `false` otherwise.

### removeContent()

Returns: `Content[]`

Removes all nodes that are immediate children of the document.

**Return:** `Content[]` - An array of all removed immediate child nodes.

### removeContent(content)

Returns: `Boolean`

Removes the given node, if the node is an immediate child of the document. The content argument can be a Content object or any node object that corresponds to a type listed in ContentTypes.

**Parameters:**
- `content` (Content) - The node to remove.

**Return:** `Boolean` - `true` if removed; `false` if not an immediate child.

### removeContent(index)

Returns: `Content`

Removes the node at the given index among all nodes that are immediate children of the document. If there is no node at the given index, this method returns null.

**Parameters:**
- `index` (Integer) - The index among immediate children.

**Return:** `Content` - The removed node, or `null` if no node exists at that index.

### setDocType(docType)

Returns: `Document`

Sets the document's DocType declaration. If the document already has a different DocType node, this method overwrites the old node. This method throws an exception if the document already contains the same DocType node that is being set.

**Parameters:**
- `docType` (DocType) - The DocType declaration to set.

**Return:** `Document` - The document, for chaining.

### setRootElement(element)

Returns: `Document`

Sets the document's root Element node. If the document already has a root Element node, this method overwrites the old node.

**Parameters:**
- `element` (Element) - The root `Element` node to set.

**Return:** `Document` - The document, for chaining.

## Properties

None.

No code samples were present on this reference page.
