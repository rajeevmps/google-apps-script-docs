# Tab

A tab within a Google Docs document.

A tab within a Google Docs document. This class allows you to retrieve tabs by ID, access tab contents as DocumentTab objects, get nested child tabs, and retrieve tab metadata including ID, index, title, and type.

## Methods

### asDocumentTab()

Returns: DocumentTab

Retrieves the tab contents as a `DocumentTab`.

**Return:** `DocumentTab` — The tab as a `DocumentTab`.

### getChildTabs()

Returns: Tab[]

Retrieves the child tabs nested within this tab.

**Return:** `Tab[]` — The child tabs nested within this tab.

**Authorization Required:** `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getId()

Returns: String

Retrieves the ID of the tab.

**Return:** `String` — The ID of the tab.

**Authorization Required:** `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getIndex()

Returns: Integer

Retrieves the 0-based index of the tab within the parent.

**Return:** `Integer` — The index of the tab within the parent.

**Authorization Required:** `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getTitle()

Returns: String

Retrieves the title of the tab.

**Return:** `String` — The title of the tab.

**Authorization Required:** `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getType()

Returns: TabType

Retrieves the type of tab. Use this method to determine the content type of this `Tab` before casting to the more specific type using `asDocumentTab()`.

```javascript
const tab = DocumentApp.getActiveDocument().getActiveTab();
if (tab.getType() === DocumentApp.TabType.DOCUMENT_TAB) {
  tab.asDocumentTab().setText('Hello World!');
}
```

**Return:** `TabType` — The tab's type.

**Authorization Required:** `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`
