# Work with tabs

## Page Summary

- Apps Script for Google Docs allows access to content from any tab within a document.
- Google Docs introduces *tabs* as an organizational layer within a single document, similar to Sheets.
- Tab properties, content, and hierarchy (including child tabs) are accessible through `Document.getTabs()` and methods of the `Tab` and `DocumentTab` classes.
- Existing methods on the `Document` class now operate on the active tab (or the first tab), and accessing content within a specific tab is recommended using `Tab.asDocumentTab()`.
- User selection, including cursor position and selection range, operates within the context of the active tab, and the active tab itself can be set using `Document.setActiveTab(tabId)`.

Google Apps Script for Google Docs lets you access content from any tab in
the document.

## What are tabs?

Docs features an organizational layer called *tabs*.
Docs allows users to create one or more tabs within a
single document, similar to how there are tabs in Sheets today. Each tab has its
own title and an ID (appended in the URL). A tab can also have *child tabs*,
which are tabs that are nested beneath another tab.

## Access Tabs

Tab properties and content are accessible with
[`Document.getTabs`](https://developers.google.com/apps-script/reference/document/document#getTabs()),
which returns a list of `Tab`s. The later sections give a brief overview of the
`Tab` class; the [Tab class documentation](https://developers.google.com/apps-script/reference/document/tab)
also provides more detailed information.

### Tab properties

Tab properties can be retrieved using methods such as
[`Tab.getId`](https://developers.google.com/apps-script/reference/document/tab#getId()) and
[`Tab.getTitle`](https://developers.google.com/apps-script/reference/document/tab#getTitle()).

### Tab contents

Document content within each tab can be retrieved using
[`Tab.asDocumentTab`](https://developers.google.com/apps-script/reference/document/tab#asDocumentTab()).
The Changes to Document Class structure
section describes how this can be used.

### Tab hierarchy

Child tabs are exposed in Apps Script through
[`Tab.getChildTabs`](https://developers.google.com/apps-script/reference/document/tab#getChildTabs()).
Accessing content from all tabs requires traversing the "tree" of child tabs.
For example, consider a document that contains a tab hierarchy as follows:

![Tablist UI containing three top-level tabs, some of which have child tabs](https://developers.google.com/static/apps-script/images/tablist.png)

In order to access *Tab 3.1.2*, do the following:

```javascript
// Print the ID of Tab 3.1.2.
const doc = DocumentApp.getActiveDocument();
const tab = doc.getTabs()[2].getChildTabs()[0].getChildTabs()[1];
console.log(tab.getId());
```

See the sample code blocks in the later sections for sample code that iterates
across all tabs in a document.

### Other ways of retrieving tabs

There are two other ways of retrieving tabs:

- [`Document.getTab`](https://developers.google.com/apps-script/reference/document/document#getTab(String)):
Returns the Tab with the specified ID.
- [`Document.getActiveTab`](https://developers.google.com/apps-script/reference/document/document#getActiveTab()):
Returns the user's active Tab. Only works in
scripts that are [bound](https://developers.google.com/apps-script/scripts_containers) to a document. The
later sections describe this in more detail.

## Changes to Document Class structure

In the past, documents did not have a concept of tabs, so the Document Class
exposed methods to directly access and modify the text contents of the document.
The following methods fall into this category:

- [`Document.addBookmark`](https://developers.google.com/apps-script/reference/document/document#addBookmark(Position))
- [`Document.addFooter`](https://developers.google.com/apps-script/reference/document/document#addFooter())
- [`Document.addHeader`](https://developers.google.com/apps-script/reference/document/document#addHeader())
- [`Document.addNamedRange`](https://developers.google.com/apps-script/reference/document/document#addNamedRange(String,Range))
- [`Document.getBody`](https://developers.google.com/apps-script/reference/document/document#getBody())
- [`Document.getBookmark`](https://developers.google.com/apps-script/reference/document/document#getBookmark(String))
- [`Document.getBookmarks`](https://developers.google.com/apps-script/reference/document/document#getBookmarks())
- [`Document.getFooter`](https://developers.google.com/apps-script/reference/document/document#getFooter())
- [`Document.getFootnotes`](https://developers.google.com/apps-script/reference/document/document#getFootnotes())
- [`Document.getHeader`](https://developers.google.com/apps-script/reference/document/document#getHeader())
- [`Document.getNamedRangeById`](https://developers.google.com/apps-script/reference/document/document#getNamedRangeById(String))
- [`Document.getNamedRanges`](https://developers.google.com/apps-script/reference/document/document#getNamedRanges())
- [`Document.getNamedRanges`](https://developers.google.com/apps-script/reference/document/document#getNamedRanges(String))
- [`Document.newPosition`](https://developers.google.com/apps-script/reference/document/document#newPosition(Element,Integer))
- [`Document.newRange`](https://developers.google.com/apps-script/reference/document/document#newRange())

With the additional structural hierarchy of tabs, these methods no longer
semantically represent the text content from all tabs in the document. The text
content will now be represented in a different layer; all of the aforementioned
text methods are accessible through `DocumentTab`.

These existing methods on the `Document` class will access or modify content
from either the active tab (in scripts [bound](https://developers.google.com/apps-script/guides/bound) to a
particular document) or the first tab (if an active one is not available).

### Access text content within a specific Tab

Instead of using the text methods off of `Document`, it is recommended to use
the methods that are available off of the `DocumentTab` class instead (which is
available through the
[`Tab.asDocumentTab`](https://developers.google.com/apps-script/reference/document/tab#asDocumentTab())
method). For example:

```javascript
// Print the text from the body of the active tab.
const doc = DocumentApp.getActiveDocument();
const documentTab = doc.getActiveTab().asDocumentTab();
const body = documentTab.getBody();
console.log(body.getText());
```

## Changes to user selection

The concept of the user's selection is only relevant and can only be used or
changed by scripts that are [bound](https://developers.google.com/apps-script/scripts_containers) to a
document.

### Text selection methods

The `Document` class provides getters and setters to manage where in the text
the user is selecting, within the active document. These methods operate within
the context of the active tab of the user running the script.

- [`Document.getCursor`](https://developers.google.com/apps-script/reference/document/document#getCursor()):
Returns the user's cursor position in the *active tab*.
- [`Document.getSelection`](https://developers.google.com/apps-script/reference/document/document#getSelection()):
Returns the user's selection range in the *active tab*.
- [`Document.setCursor`](https://developers.google.com/apps-script/reference/document/document#setCursor(Position)):
Sets the user's cursor position in the active document. If the Position is in an
inactive tab, then the user's active tab is also switched to the tab associated
with that Position.
- [`Document.setSelection`](https://developers.google.com/apps-script/reference/document/document#setSelection(Range)):
Sets the user's selection range in the active document. If the Range is in an
inactive tab, then the user's active tab is also switched to the tab associated
with that Range.

### Tab selection methods and use cases

With the introduction of tabs, get and set the active tab of the user running
the script. Use the following methods:

- [`Document.getActiveTab`](https://developers.google.com/apps-script/reference/document/document#getActiveTab()):
Returns the user's active `Tab` in the active document.
- [`Document.setActiveTab`](https://developers.google.com/apps-script/reference/document/document#setActiveTab(String)):
Sets the user's selected `Tab` in the current document to the tab with the
specified ID.

The user's holistic "selection" is made up of a combination of the active tab
along with either the current cursor position or selection range. The two
patterns for working with an active selection are to either explicitly modify
the user's active tab to a specific tab or use the user's active tab.

Explicitly change the user's active tab by using
[`Document.setActiveTab`](https://developers.google.com/apps-script/reference/document/document#setActiveTab(String)).
Alternatively, calling
[`Document.setCursor`](https://developers.google.com/apps-script/reference/document/document#setCursor(Position))
or [`Document.setSelection`](https://developers.google.com/apps-script/reference/document/document#setSelection(Range))
with a `Position` or `Range` from an inactive tab makes that tab newly active.

If the intended behavior of the script is to use the user's active tab
without changing it, then
[`Document.setActiveTab`](https://developers.google.com/apps-script/reference/document/document#setActiveTab(String))
is not necessary. The
[`Document.getCursor`](https://developers.google.com/apps-script/reference/document/document#getCursor())
and [`Document.getSelection`](https://developers.google.com/apps-script/reference/document/document#getSelection())
methods operate over the active tab, based on the tab that the user is running
the script from.

A document does not support multiple tab selections or multiple positions or
ranges across different tabs. Therefore, using
[`Document.setActiveTab`](https://developers.google.com/apps-script/reference/document/document#setActiveTab(String))
clears out the previous cursor position or selection range.

### Position and range methods for a specific Tab

The specific tab gives meaning to the text selection concepts of `Position` and
`Range`. A cursor position or a selection range is only meaningful if the
script knows the specific tab that the position or range is within.

This is achieved by using the
[`DocumentTab.newPosition`](https://developers.google.com/apps-script/reference/document/document-tab#newPosition(Element,Integer)) and
[`DocumentTab.newRange`](https://developers.google.com/apps-script/reference/document/document-tab#newRange())
methods, which construct a Position or Range that targets the specific
`DocumentTab` that the method is called from. In contrast,
[`Document.newPosition`](https://developers.google.com/apps-script/reference/document/document#newPosition(Element,Integer))
and [`Document.newRange`](https://developers.google.com/apps-script/reference/document/document#newRange())
construct a Position or Range within the active tab (or the first tab, if the
script is not bound).

See the sample code blocks in the later sections for sample code for working
with selections.

## Common usage patterns for tabs

The following code samples describe various ways of interacting with tabs.

### Read tab content from all tabs in the document

Existing code that did this before the tabs feature can be migrated to support
tabs by traversing the tabs tree and calling getter methods off of `Tab` and
`DocumentTab` instead of `Document`. The following partial code sample shows how
to print all of the text contents from every tab in a document. This tab
traversal code can be adapted for many other use cases which don't care about
the actual structure of the tabs.

```javascript
/** Logs all text contents from all tabs in the active document. */
function logAllText() {
  // Generate a list of all the tabs in the document, including any
  // nested child tabs. DocumentApp.openById('abc123456') can also
  // be used instead of DocumentApp.getActiveDocument().
  const doc = DocumentApp.getActiveDocument();
  const allTabs = getAllTabs(doc);

  // Log the content from each tab in the document.
  for (const tab of allTabs) {
    // Get the DocumentTab from the generic Tab object.
    const documentTab = tab.asDocumentTab();
    // Get the body from the given DocumentTab.
    const body = documentTab.getBody();
    // Get the body text and log it to the console.
    console.log(body.getText());
  }
}

/**
 * Returns a flat list of all tabs in the document, in the order
 * they would appear in the UI (i.e. top-down ordering). Includes
 * all child tabs.
 */
function getAllTabs(doc) {
  const allTabs = [];
  // Iterate over all tabs and recursively add any child tabs to
  // generate a flat list of Tabs.
  for (const tab of doc.getTabs()) {
    addCurrentAndChildTabs(tab, allTabs);
  }
  return allTabs;
}

/**
 * Adds the provided tab to the list of all tabs, and recurses
 * through and adds all child tabs.
 */
function addCurrentAndChildTabs(tab, allTabs) {
  allTabs.push(tab);
  for (const childTab of tab.getChildTabs()) {
    addCurrentAndChildTabs(childTab, allTabs);
  }
}
```

### Read tab content from the first tab in the document

This is similar to reading all tabs.

```javascript
/** 
 * Logs all text contents from the first tab in the active 
 * document. 
 */
function logAllText() {
  // Generate a list of all the tabs in the document, including any
  // nested child tabs.
  const doc = DocumentApp.getActiveDocument();
  const allTabs = getAllTabs(doc);

  // Log the content from the first tab in the document.
  const firstTab = allTabs[0];
  // Get the DocumentTab from the generic Tab object.
  const documentTab = firstTab.asDocumentTab();
  // Get the body from the DocumentTab.
  const body = documentTab.getBody();
  // Get the body text and log it to the console.
  console.log(body.getText());
}
```

### Update tab contents in the first tab

The following partial code sample shows how to target a specific tab when making
updates.

```javascript
/** Inserts text into the first tab of the active document. */
function insertTextInFirstTab() {
  // Get the first tab's body.
  const doc = DocumentApp.getActiveDocument();
  const firstTab = doc.getTabs()[0];
  const firstDocumentTab = firstTab.asDocumentTab();
  const firstTabBody = firstDocumentTab.getBody();

  // Append a paragraph and a page break to the first tab's body
  // section.
  firstTabBody.appendParagraph("A paragraph.");
  firstTabBody.appendPageBreak();
}
```

### Update tab contents in the active or selected tab

The following partial code sample shows how to target the active tab when making
updates.

```javascript
/**
 * Inserts text into the active/selected tab of the active
 * document.
 */
function insertTextInActiveTab() {
  // Get the active/selected tab's body.
  const doc = DocumentApp.getActiveDocument();
  const activeTab = doc.getActiveTab();
  const activeDocumentTab = activeTab.asDocumentTab();
  const activeTabBody = activeDocumentTab.getBody();

  // Append a paragraph and a page break to the active tab's body
  // section.
  activeTabBody.appendParagraph("A paragraph.");
  activeTabBody.appendPageBreak();
}
```

### Set a cursor position or selection range in the active tab

The following partial code sample shows how to update the cursor position or the
selection range within the user's active tab. This is only relevant in bound
scripts.

```javascript
/**
 * Changes the user's selection to select all tables within the tab
 * with the provided ID.
 */
function selectAllTables(tabId) {
  const doc = DocumentApp.getActiveDocument();
  const tab = doc.getTab(tabId);
  const documentTab = tab.asDocumentTab();

  // Build a range that encompasses all tables within the specified
  // tab.
  const rangeBuilder = documentTab.newRange();
  const tables = documentTab.getBody().getTables();
  for (let i = 0; i < tables.length; i++) {
    rangeBuilder.addElement(tables[i]);
  }
  // Set the document's selection to the tables within the specified
  // tab. Note that this actually switches the user's active tab as
  // well.
  doc.setSelection(rangeBuilder.build());
}
```

### Set the active or selected tab

The following partial code sample shows how to change the user's active tab.
This is only relevant in bound scripts.

```javascript
/**
 * Changes the user's selected tab to the tab immediately following
 * the currently selected one. Handles child tabs.
 *
 * Only changes the selection if there is a tab following the
 * currently selected one.
 */
function selectNextTab() {
  const doc = DocumentApp.getActiveDocument();
  const allTabs = getAllTabs(doc);
  const activeTab = doc.getActiveTab();

  // Find the index of the currently active tab.
  let activeTabIndex = -1;
  for (let i = 0; i < allTabs.length; i++) {
    if (allTabs[i].getId() === activeTab.getId()) {
      activeTabIndex = i;
    }
  }

  // Update the user's selected tab if there is a valid next tab.
  const nextTabIndex = activeTabIndex + 1;
  if (nextTabIndex < allTabs.length) {
    doc.setActiveTab(allTabs[nextTabIndex].getId());
  }
}
```
