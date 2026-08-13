# NamedRange

A range with a name and ID to allow later retrieval.

A `Range` that has a name and ID to allow later retrieval. Names are not necessarily unique; several different ranges in the same tab may share the same name, much like a class in HTML. By contrast, IDs are unique within the tab, like an ID in HTML. Once a `NamedRange` has been added to a tab, it cannot be modified, only removed.

A `NamedRange` can be accessed by any script that accesses the tab. To avoid unintended conflicts between scripts, consider prefixing range names with a unique string.

## Example

```javascript
// Create a named range that includes every table in the active tab.
const documentTab =
    DocumentApp.getActiveDocument().getActiveTab().asDocumentTab();
const rangeBuilder = documentTab.newRange();
const tables = documentTab.getBody().getTables();
for (let i = 0; i < tables.length; i++) {
  rangeBuilder.addElement(tables[i]);
}
documentTab.addNamedRange('myUniquePrefix-tables', rangeBuilder.build());
```

## Methods

### getId()

Returns: String

Gets the ID of this `NamedRange`. The ID is unique within the tab.

### getName()

Returns: String

Gets the name of this `NamedRange`. The name is not necessarily unique.

Requires authorization with one of the following scopes: `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`.

### getRange()

Returns: Range

Gets the range of elements associated with this `NamedRange`.

Requires authorization with one of the following scopes: `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`.

### remove()

Returns: void

Removes this `NamedRange` from the tab. This method doesn't delete the contents of the range; it merely removes the reference. Calling this method on a `NamedRange` that has already been removed has no effect.

Requires authorization with one of the following scopes: `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`.
