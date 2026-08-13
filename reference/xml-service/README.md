# XML Service Reference

Offline local markdown copy of the Google Apps Script XML Service reference documentation.

Source: https://developers.google.com/apps-script/reference/xml-service

## Classes and Enums

- [XmlService](./XmlService.md) - Top-level service used to parse, navigate, and programmatically create XML documents; also creates Cdata, Comment, DocType, Document, Element, Text, Namespace, and Format objects.
- [Attribute](./Attribute.md) - Represents an XML attribute; get/set its name, namespace, and value.
- [Cdata](./Cdata.md) - Represents an XML `CDATASection` node for text with special characters.
- [Comment](./Comment.md) - Represents an XML `Comment` node.
- [DocType](./DocType.md) - Represents an XML `DocumentType` node, including element name and public/system/internal subset data.
- [Document](./Document.md) - Represents an entire XML document, including its root element and DocType declaration.
- [Element](./Element.md) - Represents an XML `Element` node; provides methods for children, attributes, text, and namespaces.
- [EntityRef](./EntityRef.md) - Represents an XML `EntityReference` node.
- [Format](./Format.md) - A formatter for outputting an XML document (compact, pretty, or raw), with customizable encoding, indentation, and line separators.
- [Namespace](./Namespace.md) - Represents an XML namespace (prefix and URI).
- [ProcessingInstruction](./ProcessingInstruction.md) - Represents an XML `ProcessingInstruction` node.
- [Text](./Text.md) - Represents an XML `Text` node.
- [Content](./Content.md) - A generic representation of any XML node type (implemented by Cdata, Comment, DocType, Element, EntityRef, ProcessingInstruction, and Text); provides `as*()` casting methods and `getType()`.
- [ContentType](./ContentType.md) - Enum (named `ContentTypes` on the live site) of the possible XML content node types: CDATA, COMMENT, DOCTYPE, ELEMENT, ENTITYREF, PROCESSINGINSTRUCTION, TEXT.
