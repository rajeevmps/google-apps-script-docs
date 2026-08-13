# Document Service Reference

Offline local markdown copy of the Google Apps Script **Document** (Google Docs) service reference documentation, sourced from https://developers.google.com/apps-script/reference/document.

## Core / Entry Points

- [DocumentApp](./DocumentApp.md) — The document service creates and opens Documents that can be edited.
- [Document](./Document.md) — A document, containing one or more Tab objects, each of which contains rich text and elements such as tables and lists.
- [DocumentTab](./DocumentTab.md) — A document tab, containing rich text and elements such as tables and lists.
- [Tab](./Tab.md) — A tab within a Google Docs document.
- [Body](./Body.md) — The Body represents the content of a tab in a Google Docs document.

## Ranges & Positions

- [Range](./Range.md) — A range of elements in a document.
- [RangeBuilder](./RangeBuilder.md) — A builder used to construct Range objects from document elements.
- [RangeElement](./RangeElement.md) — A wrapper around an Element with a possible start and end offset.
- [Position](./Position.md) — A Position represents a location in a document relative to a specific element.
- [NamedRange](./NamedRange.md) — A range with a name and ID to allow later retrieval.

## Base Element Types

- [Element](./Element.md) — A generic element.
- [ContainerElement](./ContainerElement.md) — A generic element that may contain other elements.
- [Attribute](./Attribute.md) — An enumeration of the element attributes.

## Structural Elements

- [Paragraph](./Paragraph.md) — An element representing a paragraph.
- [ListItem](./ListItem.md) — An element representing a list item.
- [Text](./Text.md) — An element representing a rich text region.
- [Table](./Table.md) — An element representing a table.
- [TableRow](./TableRow.md) — An element representing a table row.
- [TableCell](./TableCell.md) — An element representing a table cell.
- [TableOfContents](./TableOfContents.md) — An element containing a table of contents.
- [HeaderSection](./HeaderSection.md) — An element representing a header section.
- [FooterSection](./FooterSection.md) — An element representing a footer section.
- [Footnote](./Footnote.md) — An element representing a footnote within a document.
- [FootnoteSection](./FootnoteSection.md) — An element representing a footnote section.
- [HorizontalRule](./HorizontalRule.md) — An element representing a horizontal rule.
- [PageBreak](./PageBreak.md) — An element representing a page break.
- [Bookmark](./Bookmark.md) — A Bookmark object represents a bookmark in a Google Document.
- [InlineImage](./InlineImage.md) — An element representing an embedded image.
- [InlineDrawing](./InlineDrawing.md) — An element representing an embedded drawing.
- [PositionedImage](./PositionedImage.md) — Fixed position image anchored to a Paragraph.
- [Date](./Date.md) — An element representing a formatted date.
- [Person](./Person.md) — An element representing a link to a person.
- [RichLink](./RichLink.md) — An element representing a link to a Google resource, such as a Drive file or a YouTube video.
- [UnsupportedElement](./UnsupportedElement.md) — An element representing a region that is unknown or cannot be affected by a script, such as a page number.

## Equations

- [Equation](./Equation.md) — An element representing a mathematical expression.
- [EquationFunction](./EquationFunction.md) — An element representing a function in a mathematical Equation.
- [EquationFunctionArgumentSeparator](./EquationFunctionArgumentSeparator.md) — An element representing a function separator in a mathematical Equation.
- [EquationSymbol](./EquationSymbol.md) — An element representing a symbol within a mathematical Equation.

## Enums

- [ElementType](./ElementType.md) — Enumeration listing all possible element types in a document.
- [FontFamily](./FontFamily.md) — Deprecated enumeration of supported font families.
- [GlyphType](./GlyphType.md) — Enumeration defining supported glyph types for list items.
- [HorizontalAlignment](./HorizontalAlignment.md) — Enumeration of supported horizontal alignment types.
- [ParagraphHeading](./ParagraphHeading.md) — Enumeration used to configure the heading style for a ParagraphElement.
- [PositionedLayout](./PositionedLayout.md) — Enumeration that specifies how to lay out a PositionedImage in relation to surrounding text.
- [TabType](./TabType.md) — Enumeration of all the tab types available in DocumentApp.
- [TextAlignment](./TextAlignment.md) — Enumeration used to specify text alignment types.
- [VerticalAlignment](./VerticalAlignment.md) — Enumeration of supported vertical alignment types.

---

47 classes/enums, one markdown file each, fetched verbatim from the official Apps Script reference documentation.
