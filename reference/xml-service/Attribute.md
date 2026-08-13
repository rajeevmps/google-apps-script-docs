# Attribute

A representation of an XML attribute.

A representation of an XML attribute. The Attribute object represents an XML attribute and is used in conjunction with XmlService. Attributes have methods to get and set their name, namespace, and value.

## Methods

### getName()

Returns: `String`

Gets the local name of the attribute. If the attribute has a namespace prefix, use `getNamespace().getPrefix()` to get the prefix.

**Return:** `String` - The local name of the attribute.

### getNamespace()

Returns: `Namespace`

Gets the namespace for the attribute.

**Return:** `Namespace` - The namespace for the attribute.

### getValue()

Returns: `String`

Gets the value of the attribute.

**Return:** `String` - The value of the attribute.

### setName(name)

Returns: `Attribute`

Sets the local name of the attribute. To set a namespace prefix for the attribute, use `setNamespace(namespace)` in conjunction with `XmlService.getNamespace(prefix, uri)`.

**Parameters:**
- `name` (String) - The local name to set.

**Return:** `Attribute` - The attribute, for chaining.

### setNamespace(namespace)

Returns: `Attribute`

Sets the namespace for the attribute. The namespace must have a prefix.

**Parameters:**
- `namespace` (Namespace) - The namespace to set.

**Return:** `Attribute` - The attribute, for chaining.

### setValue(value)

Returns: `Attribute`

Sets the value of the attribute.

**Parameters:**
- `value` (String) - The value to set.

**Return:** `Attribute` - The attribute, for chaining.

## Properties

None.

## Code Sample

```javascript
let xml = '<roster>' +
    '<person first="John" last="Doe"/>' +
    '<person first="Mary" last="Smith"/>' +
    '</roster>';
const document = XmlService.parse(xml);
const people = document.getRootElement().getChildren('person');
for (let i = 0; i < people.length; i++) {
  const person = people[i];
  const firstName = person.getAttribute('first').getValue();
  const lastName = person.getAttribute('last').getValue();
  person.setAttribute('full', `${firstName} ${lastName}`);
}
xml = XmlService.getPrettyFormat().format(document);
Logger.log(xml);
```
