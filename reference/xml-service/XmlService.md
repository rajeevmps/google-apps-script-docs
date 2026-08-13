# XmlService

This service allows scripts to parse, navigate, and programmatically create XML documents.

This service allows scripts to parse, navigate, and programmatically create XML documents.

## Methods

### createCdata(text)

Returns: `Cdata`

Creates an unattached `CDATASection` node with the given value.

**Parameters:**
- `text` (String) - The value to set.

**Return:** `Cdata` - The newly created `CDATASection` node.

### createComment(text)

Returns: `Comment`

Creates an unattached `Comment` node with the given value.

**Parameters:**
- `text` (String) - The value to set.

**Return:** `Comment` - The newly created `Comment` node.

### createDocType(elementName)

Returns: `DocType`

Creates an unattached `DocumentType` node for the root `Element` node with the given name.

**Parameters:**
- `elementName` (String) - The name of the root `Element` node to specify in the `DocType` declaration.

**Return:** `DocType` - The newly created `DocumentType` node.

### createDocType(elementName, systemId)

Returns: `DocType`

Creates an unattached `DocumentType` node for the root `Element` node with the given name, and the given system ID for the external subset data.

**Parameters:**
- `elementName` (String) - The name of the root `Element` node to specify in the `DocType` declaration.
- `systemId` (String) - The system ID of the external subset data to set.

**Return:** `DocType` - The newly created `DocumentType` node.

### createDocType(elementName, publicId, systemId)

Returns: `DocType`

Creates an unattached `DocumentType` node for the root `Element` node with the given name, and the given public ID and system ID for the external subset data.

**Parameters:**
- `elementName` (String) - The name of the root `Element` node to specify in the `DocType` declaration.
- `publicId` (String) - The public ID of the external subset data to set.
- `systemId` (String) - The system ID of the external subset data to set.

**Return:** `DocType` - The newly created `DocumentType` node.

### createDocument()

Returns: `Document`

Creates an empty XML document.

**Return:** `Document` - The newly created document.

### createDocument(rootElement)

Returns: `Document`

Creates an XML document with the given root `Element` node.

**Parameters:**
- `rootElement` (Element) - The root `Element` node to set.

**Return:** `Document` - The newly created document.

### createElement(name)

Returns: `Element`

Creates an unattached `Element` node with the given local name and no namespace.

**Parameters:**
- `name` (String) - The local name to set.

**Return:** `Element` - The newly created `Element` node.

### createElement(name, namespace)

Returns: `Element`

Creates an unattached `Element` node with the given local name and namespace.

**Parameters:**
- `name` (String) - The local name to set.
- `namespace` (Namespace) - The namespace to set.

**Return:** `Element` - The newly created `Element` node.

### createText(text)

Returns: `Text`

Creates an unattached `Text` node with the given value.

**Parameters:**
- `text` (String) - The value to set.

**Return:** `Text` - The newly created `Text` node.

### getCompactFormat()

Returns: `Format`

Creates a `Format` object for outputting a compact XML document. The formatter defaults to `UTF-8` encoding, no indentation, and no additional line breaks, but includes the XML declaration and its encoding.

**Return:** `Format` - The newly created formatter.

### getNamespace(uri)

Returns: `Namespace`

Creates a `Namespace` with the given URI.

**Parameters:**
- `uri` (String) - The URI for the namespace.

**Return:** `Namespace` - The newly created namespace.

### getNamespace(prefix, uri)

Returns: `Namespace`

Creates a `Namespace` with the given prefix and URI.

**Parameters:**
- `prefix` (String) - The prefix for the namespace.
- `uri` (String) - The URI for the namespace.

**Return:** `Namespace` - The newly created namespace.

### getNoNamespace()

Returns: `Namespace`

Creates a `Namespace` that represents the absence of a real namespace.

**Return:** `Namespace` - The newly created namespace.

### getPrettyFormat()

Returns: `Format`

Creates a `Format` object for outputting a human-readable XML document. The formatter defaults to `UTF-8` encoding, two-space indentation, `\r\n` line separators after every node, and includes the XML declaration and its encoding.

**Return:** `Format` - The newly created formatter.

### getRawFormat()

Returns: `Format`

Creates a `Format` object for outputting a raw XML document. The formatter defaults to `UTF-8` encoding, no indentation and no line breaks other than those provided in the XML document itself, and includes the XML declaration and its encoding.

**Return:** `Format` - The newly created formatter.

### getXmlNamespace()

Returns: `Namespace`

Creates a `Namespace` with the standard `xml` prefix.

**Return:** `Namespace` - The newly created namespace.

### parse(xml)

Returns: `Document`

Creates an `Document` from the given XML, without validating the XML.

**Parameters:**
- `xml` (String) - The XML to parse.

**Return:** `Document` - The newly created document.

## Properties

None.

## Code Samples

**Sample 1: Parsing XML**
```javascript
// Log the title and labels for the first page of blog posts on the
// Google Workspace Developer blog.
function parseXml() {
  const url = 'https://gsuite-developers.googleblog.com/atom.xml';
  const xml = UrlFetchApp.fetch(url).getContentText();
  const document = XmlService.parse(xml);
  const root = document.getRootElement();
  const atom = XmlService.getNamespace('http://www.w3.org/2005/Atom');

  const entries = root.getChildren('entry', atom);
  for (let i = 0; i < entries.length; i++) {
    const title = entries[i].getChild('title', atom).getText();
    const categoryElements = entries[i].getChildren('category', atom);
    const labels = [];
    for (let j = 0; j < categoryElements.length; j++) {
      labels.push(categoryElements[j].getAttribute('term').getValue());
    }
    Logger.log('%s (%s)', title, labels.join(', '));
  }
}
```

**Sample 2: Creating XML**
```javascript
// Create and log an XML representation of the threads in your Gmail inbox.
function createXml() {
  const root = XmlService.createElement('threads');
  const threads = GmailApp.getInboxThreads();
  for (let i = 0; i < threads.length; i++) {
    const child =
        XmlService.createElement('thread')
            .setAttribute('messageCount', threads[i].getMessageCount())
            .setAttribute('isUnread', threads[i].isUnread())
            .setText(threads[i].getFirstMessageSubject());
    root.addContent(child);
  }
  const document = XmlService.createDocument(root);
  const xml = XmlService.getPrettyFormat().format(document);
  Logger.log(xml);
}
```
