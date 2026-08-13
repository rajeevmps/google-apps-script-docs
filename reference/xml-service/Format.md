# Format

A formatter for outputting an XML document, with three pre-defined formats that can be further customized.

A formatter for outputting an XML document, with three pre-defined formats that can be further customized.

## Methods

### format(document)

Returns: `String`

Outputs the given Document as a formatted string.

**Parameters:**
- `document` (Document) - The document to format.

**Return:** `String` - The formatted document.

### format(element)

Returns: `String`

Outputs the given Element node as a formatted string.

**Parameters:**
- `element` (Element) - The element to format.

**Return:** `String` - The formatted element.

### setEncoding(encoding)

Returns: `Format`

Sets the character encoding that the formatter should use. The encoding argument must be an accepted XML encoding like ISO-8859-1, US-ASCII, UTF-8, or UTF-16.

**Parameters:**
- `encoding` (String) - The encoding to use.

**Return:** `Format` - The formatter, for chaining.

### setIndent(indent)

Returns: `Format`

Sets the string used to indent child nodes relative to their parents. Setting an indent other than null will cause the formatter to insert a line break after every node.

**Parameters:**
- `indent` (String) - The indent to use.

**Return:** `Format` - The formatter, for chaining.

### setLineSeparator(separator)

Returns: `Format`

Sets the string to insert whenever the formatter would normally insert a line break. The three pre-defined formatters have different conditions under which they insert a line break. The default line separator is \r\n.

**Parameters:**
- `separator` (String) - The separator to use.

**Return:** `Format` - The formatter, for chaining.

### setOmitDeclaration(omitDeclaration)

Returns: `Format`

Sets whether the formatter should omit the XML declaration, such as `<?xml version="1.0" encoding="UTF-8"?>`.

**Parameters:**
- `omitDeclaration` (Boolean) - true to omit the XML declaration; false to include it.

**Return:** `Format` - The formatter, for chaining.

### setOmitEncoding(omitEncoding)

Returns: `Format`

Sets whether the formatter should omit the encoding in the XML declaration, such as the encoding field in `<?xml version="1.0" encoding="UTF-8"?>`.

**Parameters:**
- `omitEncoding` (Boolean) - true to omit the encoding in the XML declaration; false to include it.

**Return:** `Format` - The formatter, for chaining.

## Properties

None.

## Code Sample

```javascript
const xml = '<root><a><b>Text!</b><b>More text!</b></a></root>';
const document = XmlService.parse(xml);
const output = XmlService.getCompactFormat()
                   .setLineSeparator('\n')
                   .setEncoding('UTF-8')
                   .setIndent('   ')
                   .format(document);
Logger.log(output);
```
