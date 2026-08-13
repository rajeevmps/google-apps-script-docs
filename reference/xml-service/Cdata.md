# Cdata

A representation of an XML `CDATASection` node.

A representation of an XML `CDATASection` node. Special characters are stored differently in `CDATASection` nodes compared to Text nodes. Methods are available to manipulate Cdata nodes, such as appending text, detaching from a parent, getting the parent element, and getting or setting the text value.

## Methods

### append(text)

Returns: `Text`

Appends the given text to any content that already exists in the node.

**Parameters:**
- `text` (String) - The text to append to the node.

**Return:** `Text` - node, for chaining.

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

Gets the text value of all nodes that are direct or indirect children of the node, in the order they appear in the document.

**Return:** `String` - The text value of all nodes that are direct or indirect children of the node.

### setText(text)

Returns: `Text`

Sets the text value of the `Text` node.

**Parameters:**
- `text` (String) - The text value to set.

**Return:** `Text` - The `Text` node, for chaining.

## Properties

None.

## Code Sample

```javascript
const illegalCharacters = '<em>The Amazing Adventures of Kavalier & Clay</em>';
const cdata = XmlService.createCdata(illegalCharacters);
const text = XmlService.createText(illegalCharacters);
const root = XmlService.createElement('root').addContent(cdata).addContent(text);
const document = XmlService.createDocument(root);
const xml = XmlService.getPrettyFormat().format(document);
Logger.log(xml);
```
