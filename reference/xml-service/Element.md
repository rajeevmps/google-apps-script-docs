# Element

A representation of an XML `Element` node.

A representation of an XML `Element` node. The Element object represents an XML Element node and provides methods for manipulating its content, attributes, and relationships within an XML document. You can add, remove, and retrieve content (including child elements and other nodes) from an Element using methods like addContent, removeContent, getAllContent, getChildren, and getContent. Attributes of an Element can be accessed, set, and removed using methods like getAttribute, getAttributes, setAttribute, and removeAttribute. The name and text value of an Element can be retrieved and set using getName, getQualifiedName, getText, setText, and getValue. Methods are available to check the parent and document of an Element, determine if it is the root element, and detach it from its parent.

## Methods

### addContent(content)

Returns: `Element`

Appends the given node as the last child of the `Element` node. The `content` argument can be a `Element` object or any node object that corresponds to a type listed in `ContentTypes`.

**Parameters:**
- `content` (Content) - The node to append.

**Return:** `Element` - The `Element` node, for chaining.

### addContent(index, content)

Returns: `Element`

Inserts the given node at the given index among all nodes that are immediate children of the `Element` node. The `content` argument can be a `Element` object or any node object that corresponds to a type listed in `ContentTypes`.

**Parameters:**
- `index` (Integer) - The index at which to insert the node among immediate children.
- `content` (Content) - The node to insert.

**Return:** `Element` - The `Element` node, for chaining.

### cloneContent()

Returns: `Content[]`

Creates unattached copies of all nodes that are immediate children of the Element node.

**Return:** `Content[]` - An array of unattached copies of all immediate child nodes.

### detach()

Returns: `Content`

Detaches the node from its parent `Element` node. If the node does not have a parent, this method has no effect.

**Return:** `Content` - The detached node.

### getAllContent()

Returns: `Content[]`

Gets all nodes that are immediate children of the Element node.

**Return:** `Content[]` - An array of all immediate child nodes.

### getAttribute(name)

Returns: `Attribute`

Gets the attribute for this `Element` node with the given name and no namespace. If there is no such attribute, this method returns `null`.

**Parameters:**
- `name` (String) - The name of the attribute.

**Return:** `Attribute` - The attribute, or `null` if none exists.

### getAttribute(name, namespace)

Returns: `Attribute`

Gets the attribute for this `Element` node with the given name and namespace. If there is no such node, this method returns `null`.

**Parameters:**
- `name` (String) - The name of the attribute.
- `namespace` (Namespace) - The namespace of the attribute.

**Return:** `Attribute` - The attribute, or `null` if none exists.

### getAttributes()

Returns: `Attribute[]`

Gets all attributes for this `Element` node, in the order they appear in the document.

**Return:** `Attribute[]` - An array of all attributes for this `Element` node.

### getChild(name)

Returns: `Element`

Gets the first `Element` node with the given name and no namespace that is an immediate child of this `Element` node. If there is no such node, this method returns `null`.

**Parameters:**
- `name` (String) - The name of the child `Element` node.

**Return:** `Element` - The `Element` node, or `null` if none exists.

### getChild(name, namespace)

Returns: `Element`

Gets the first `Element` node with the given name and namespace that is an immediate child of this `Element` node. If there is no such node, this method returns `null`.

**Parameters:**
- `name` (String) - The name of the child `Element` node.
- `namespace` (Namespace) - The namespace of the child `Element` node.

**Return:** `Element` - The `Element` node, or `null` if none exists.

### getChildText(name)

Returns: `String`

Gets the text value of the node with the given name and no namespace, if the node is an immediate child of the `Element` node. If there is no such node, this method returns `null`.

**Parameters:**
- `name` (String) - The name of the child node.

**Return:** `String` - The text value of the child node, or `null` if none exists.

### getChildText(name, namespace)

Returns: `String`

Gets the text value of the node with the given name and namespace, if the node is an immediate child of the `Element` node. If there is no such node, this method returns `null`.

**Parameters:**
- `name` (String) - The name of the child node.
- `namespace` (Namespace) - The namespace of the child node.

**Return:** `String` - The text value of the child node, or `null` if none exists.

### getChildren()

Returns: `Element[]`

Gets all `Element` nodes that are immediate children of this `Element` node, in the order they appear in the document.

**Return:** `Element[]` - An array of all immediate child `Element` nodes.

### getChildren(name)

Returns: `Element[]`

Gets all `Element` nodes with the given name and no namespace that are immediate children of this `Element` node, in the order they appear in the document.

**Parameters:**
- `name` (String) - The name of the child `Element` nodes.

**Return:** `Element[]` - An array of all matching immediate child `Element` nodes.

### getChildren(name, namespace)

Returns: `Element[]`

Gets all `Element` nodes with the given name and namespace that are immediate children of this `Element` node, in the order they appear in the document.

**Parameters:**
- `name` (String) - The name of the child `Element` nodes.
- `namespace` (Namespace) - The namespace of the child `Element` nodes.

**Return:** `Element[]` - An array of all matching immediate child `Element` nodes.

### getContent(index)

Returns: `Content`

Gets the node at the given index among all nodes that are immediate children of the Element node. If there is no node at the given index, this method returns `null`.

**Parameters:**
- `index` (Integer) - The index for the node among immediate children.

**Return:** `Content` - The node, or `null` if none exists at that index.

### getContentSize()

Returns: `Integer`

Gets the number of nodes that are immediate children of the Element node.

**Return:** `Integer` - The count of immediate child nodes.

### getDescendants()

Returns: `Content[]`

Gets all nodes that are direct or indirect children of the Element node, in the order they appear in the document.

**Return:** `Content[]` - An array of all descendant nodes.

### getDocument()

Returns: `Document`

Gets the XML document that contains the Element node.

**Return:** `Document` - The document containing this `Element` node.

### getName()

Returns: `String`

Gets the local name of the `Element` node. If the node has a namespace prefix, use `getQualifiedName()` or `getNamespace().getPrefix()` to get the prefix.

**Return:** `String` - The local name of the `Element` node.

### getNamespace()

Returns: `Namespace`

Gets the namespace for the `Element` node.

**Return:** `Namespace` - The namespace for the `Element` node.

### getNamespace(prefix)

Returns: `Namespace`

Gets the namespace with the given prefix for the `Element` node.

**Parameters:**
- `prefix` (String) - The prefix for the namespace.

**Return:** `Namespace` - The namespace with the given prefix.

### getParentElement()

Returns: `Element`

Gets the node's parent `Element` node. If the node does not have a parent, this method returns `null`.

**Return:** `Element` - The parent `Element` node, or `null` if none exists.

### getQualifiedName()

Returns: `String`

Gets the local name and namespace prefix of the `Element` node, in the form `[namespacePrefix]:[localName]`. If the node does not have a namespace prefix, use `getName()`.

**Return:** `String` - The qualified name in the form `[namespacePrefix]:[localName]`.

### getText()

Returns: `String`

Gets the text value of the `Element` node.

**Return:** `String` - The text value of the `Element` node.

### getValue()

Returns: `String`

Gets the text value of all nodes that are direct or indirect children of the node, in the order they appear in the document.

**Return:** `String` - The text value of all descendant nodes.

### isAncestorOf(other)

Returns: `Boolean`

Determines whether this `Element` node is a direct or indirect parent of a given `Element` node.

**Parameters:**
- `other` (Element) - The other `Element` node.

**Return:** `Boolean` - `true` if this node is an ancestor; `false` otherwise.

### isRootElement()

Returns: `Boolean`

Determines whether the `Element` node is the document's root node.

**Return:** `Boolean` - `true` if this is the root element; `false` otherwise.

### removeAttribute(attribute)

Returns: `Boolean`

Removes the given attribute for this `Element` node, if such an attribute exists.

**Parameters:**
- `attribute` (Attribute) - The attribute to remove.

**Return:** `Boolean` - `true` if removed; `false` if not found.

### removeAttribute(attributeName)

Returns: `Boolean`

Removes the attribute for this `Element` node with the given name and no namespace, if such an attribute exists.

**Parameters:**
- `attributeName` (String) - The name of the attribute.

**Return:** `Boolean` - `true` if removed; `false` if not found.

### removeAttribute(attributeName, namespace)

Returns: `Boolean`

Removes the attribute for this `Element` node with the given name and namespace, if such an attribute exists.

**Parameters:**
- `attributeName` (String) - The name of the attribute.
- `namespace` (Namespace) - The namespace of the attribute.

**Return:** `Boolean` - `true` if removed; `false` if not found.

### removeContent()

Returns: `Content[]`

Removes all nodes that are immediate children of the Element node.

**Return:** `Content[]` - An array of all removed immediate child nodes.

### removeContent(content)

Returns: `Boolean`

Removes the given node, if the node is an immediate child of the Element node. The `content` argument can be a `Element` object or any node object that corresponds to a type listed in `ContentTypes`.

**Parameters:**
- `content` (Content) - The node to remove.

**Return:** `Boolean` - `true` if removed; `false` if not an immediate child.

### removeContent(index)

Returns: `Content`

Removes the node at the given index among all nodes that are immediate children of the Element node. If there is no node at the given index, this method returns `null`.

**Parameters:**
- `index` (Integer) - The index among immediate children.

**Return:** `Content` - The removed node, or `null` if no node exists at that index.

### setAttribute(attribute)

Returns: `Element`

Sets the given attribute for this `Element` node.

**Parameters:**
- `attribute` (Attribute) - The attribute to set.

**Return:** `Element` - The `Element` node, for chaining.

### setAttribute(name, value)

Returns: `Element`

Sets the attribute for this `Element` node with the given name, value, and no namespace.

**Parameters:**
- `name` (String) - The name of the attribute to set.
- `value` (String) - The value of the attribute to set.

**Return:** `Element` - The `Element` node, for chaining.

### setAttribute(name, value, namespace)

Returns: `Element`

Sets the attribute for this `Element` node with the given name, value, and namespace.

**Parameters:**
- `name` (String) - The name of the attribute to set.
- `value` (String) - The value of the attribute to set.
- `namespace` (Namespace) - The namespace of the attribute to set.

**Return:** `Element` - The `Element` node, for chaining.

### setName(name)

Returns: `Element`

Sets the local name of the `Element` node. To set a namespace prefix for the node, use `setNamespace(namespace)` in conjunction with `XmlService.getNamespace(prefix, uri)`.

**Parameters:**
- `name` (String) - The local name to set.

**Return:** `Element` - The `Element` node, for chaining.

### setNamespace(namespace)

Returns: `Element`

Sets the namespace for the `Element` node.

**Parameters:**
- `namespace` (Namespace) - The namespace to set.

**Return:** `Element` - The `Element` node, for chaining.

### setText(text)

Returns: `Element`

Sets the text value of the `Element` node. If the node already contains a text value or any child nodes, this method overwrites the old content. To append or insert content instead, use `addContent(content)` or `addContent(index, content)`.

**Parameters:**
- `text` (String) - The text to set.

**Return:** `Element` - The `Element` node, for chaining.

## Properties

None.

## Code Sample

```javascript
let xml = '<things>' +
    '<plates>12</plates>' +
    '<bowls>18</bowls>' +
    '<cups>25</cups>' +
    '</things>';
const document = XmlService.parse(xml);
const root = document.getRootElement();
const items = root.getChildren();
let total = 0;
for (let i = 0; i < items.length; i++) {
  total += Number(items[i].getText());
}
const totalElement = XmlService.createElement('total').setText(total);
root.addContent(totalElement);
xml = XmlService.getPrettyFormat().format(document);
Logger.log(xml);
```
