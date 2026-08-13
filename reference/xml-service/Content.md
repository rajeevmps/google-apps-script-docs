# Content

A representation of a generic XML node.

A representation of a generic XML node. The interface has implementing classes for various XML node types including Cdata, Comment, DocType, Element, EntityRef, ProcessingInstruction, and Text.

## Methods

### asCdata()

Returns: `Cdata`

Casts the node as a `CDATASection` node for the purposes of autocomplete. If the node's `ContentTypes` is not already `CDATA`, this method returns `null`.

**Return:** `Cdata` - The `CDATASection` node.

### asComment()

Returns: `Comment`

Casts the node as a `Comment` node for the purposes of autocomplete. If the node's `ContentTypes` is not already `COMMENT`, this method returns `null`.

**Return:** `Comment` - The `Comment` node, or `null` if the node's content type is not `COMMENT`.

### asDocType()

Returns: `DocType`

Casts the node as a `DocumentType` node for the purposes of autocomplete. If the node's `ContentTypes` is not already `DOCTYPE`, this method returns `null`.

**Return:** `DocType` - The `DocumentType` node.

### asElement()

Returns: `Element`

Casts the node as an `Element` node for the purposes of autocomplete. If the node's `ContentTypes` is not already `ELEMENT`, this method returns `null`.

**Return:** `Element` - The `Element` node.

### asEntityRef()

Returns: `EntityRef`

Casts the node as a `EntityReference` node for the purposes of autocomplete. If the node's `ContentTypes` is not already `ENTITYREF`, this method returns `null`.

**Return:** `EntityRef` - The `EntityReference` node.

### asProcessingInstruction()

Returns: `ProcessingInstruction`

Casts the node as a `ProcessingInstruction` node for the purposes of autocomplete. If the node's `ContentTypes` is not already `PROCESSINGINSTRUCTION`, this method returns `null`.

**Return:** `ProcessingInstruction` - The `ProcessingInstruction` node.

### asText()

Returns: `Text`

Casts the node as a `Text` node for the purposes of autocomplete. If the node's `ContentTypes` is not already `TEXT`, this method returns `null`.

**Return:** `Text` - The `Text` node.

### detach()

Returns: `Content`

Detaches the node from its parent `Element` node. If the node does not have a parent, this method has no effect.

**Return:** `Content` - The detached node.

### getParentElement()

Returns: `Element`

Gets the node's parent `Element` node. If the node does not have a parent, this method returns `null`.

**Return:** `Element` - The parent `Element` node.

### getType()

Returns: `ContentTypes`

Gets the node's content type.

**Return:** `ContentTypes` - The node's content type.

### getValue()

Returns: `String`

Gets the text value of all nodes that are direct or indirect children of the node, in the order they appear in the document.

**Return:** `String` - The text value of all nodes that are direct or indirect children of the node.

## Properties

None.

No code samples were provided on this reference page.
