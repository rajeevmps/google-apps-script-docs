# DocumentApp

The document service creates and opens Documents that can be edited.

The document service creates and opens `Documents` that can be edited.

## Example

```javascript
// Open a document by ID.
// TODO(developer): Replace the ID with your own.
let doc = DocumentApp.openById('DOCUMENT_ID');

// Create and open a document.
doc = DocumentApp.create('Document Name');
```

## Methods

### create(name)

Returns: Document

Creates and returns a new document.

**Parameters:**
- `name` (String) — The new document's name.

**Authorization Required:** `https://www.googleapis.com/auth/documents`

### getActiveDocument()

Returns: Document

Returns the document to which the script is container-bound. To interact with document to which the script is not container-bound, use `openById(id)` or `openByUrl(url)` instead.

**Authorization Required:** `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getUi()

Returns: Ui

Returns an instance of the document's user-interface environment that allows the script to add features like menus, dialogs, and sidebars. A script can only interact with the UI for the current instance of an open document, and only if the script is bound to the document.

### openById(id)

Returns: Document

Returns the document with the specified ID. If the script is container-bound to the document, use `getActiveDocument()` instead.

**Parameters:**
- `id` (String) — The ID of the document to open.

**Authorization Required:** `https://www.googleapis.com/auth/documents`

### openByUrl(url)

Returns: Document

Opens and returns the document with the specified URL. If the script is container-bound to the document, use `getActiveDocument()` instead.

**Parameters:**
- `url` (String) — the URL of the document to open

**Authorization Required:** `https://www.googleapis.com/auth/documents`

## Properties

| Property | Type | Description |
|----------|------|-------------|
| `Attribute` | `Attribute` | The `Attribute` enumeration. |
| `ElementType` | `ElementType` | The `ElementType` enumeration. |
| `FontFamily` | `FontFamily` | The `FontFamily` enumeration. |
| `GlyphType` | `GlyphType` | The `GlyphType` enumeration. |
| `HorizontalAlignment` | `HorizontalAlignment` | The `HorizontalAlignment` enumeration. |
| `ParagraphHeading` | `ParagraphHeading` | The `ParagraphHeading` enumeration. |
| `PositionedLayout` | `PositionedLayout` | The `PositionedLayout` enumeration. |
| `TextAlignment` | `TextAlignment` | The `TextAlignment` enumeration. |
| `VerticalAlignment` | `VerticalAlignment` | The `VerticalAlignment` enumeration. |
