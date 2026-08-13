# Bookmark

A Bookmark object represents a bookmark in a Google Document.

A Bookmark object represents a bookmark in a Google Document. You can add a bookmark at the cursor position in the active document tab. Bookmark objects have methods to get their ID and position, and to remove themselves.

## Example

```javascript
const doc = DocumentApp.getActiveDocument();
const documentTab = doc.getActiveTab().asDocumentTab();

// Insert a bookmark at the cursor position (in the active tab) and log its ID.
const cursor = doc.getCursor();
const bookmark = documentTab.addBookmark(cursor);
Logger.log(bookmark.getId());
```

## Methods

| Method | Return Type | Brief Description |
|--------|-------------|-------------------|
| `getId()` | `String` | Gets the ID of the `Bookmark`. |
| `getPosition()` | `Position` | Gets the `Position` of the `Bookmark` within the `DocumentTab`. |
| `remove()` | `void` | Deletes the `Bookmark`. |

### getId()

Returns: String

Gets the ID of the `Bookmark`. The ID is unique within the `DocumentTab`. Returns the `Bookmark`'s ID, which is unique within the DocumentTab.

Authorization: Scripts require one or more of the following scopes:
- `https://www.googleapis.com/auth/documents.currentonly`
- `https://www.googleapis.com/auth/documents`

### getPosition()

Returns: Position

Gets the `Position` of the `Bookmark` within the `DocumentTab`. The `Position` remains accurate so long as the `Bookmark` is not deleted, even if the script changes the document structure.

Authorization: Scripts require one or more of the following scopes:
- `https://www.googleapis.com/auth/documents.currentonly`
- `https://www.googleapis.com/auth/documents`

### remove()

Returns: void

Deletes the `Bookmark`. Calling this method on a `Bookmark` that has already been deleted has no effect.

Authorization: Scripts require one or more of the following scopes:
- `https://www.googleapis.com/auth/documents.currentonly`
- `https://www.googleapis.com/auth/documents`

## Properties

None.
