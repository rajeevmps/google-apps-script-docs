# Document

A document, containing one or more Tab objects, each of which contains rich text and elements such as tables and lists.

A document, containing one or more Tab objects, each of which contains rich text and elements such as tables and lists. Documents may be opened or created using DocumentApp.

Methods on the Document class that directly access and modify text contents operate on either the active tab (in scripts bound to a particular document) or the first tab (if an active one isn't available).

## Methods

### addBookmark(position)

Returns: Bookmark

Adds a Bookmark at the given Position to the first tab or, for scripts that are bound to a document, the active tab.

### addEditor(emailAddress)

Returns: Document

Adds the given user to the list of editors for the Document. If the user was already on the list of viewers, this method promotes the user out of the list of viewers.

### addEditor(user)

Returns: Document

Adds the given user to the list of editors for the Document. If the user was already on the list of viewers, this method promotes the user out of the list of viewers.

### addEditors(emailAddresses)

Returns: Document

Adds the given array of users to the list of editors for the Document. If any of the users were already on the list of viewers, this method promotes them out of the list of viewers.

### addFooter()

Returns: FooterSection

Adds a footer section, if none exists, to the first tab or, for scripts that are bound to a document, the active tab.

### addHeader()

Returns: HeaderSection

Adds a header section, if none exists, to the first tab or, for scripts that are bound to a document, the active tab.

### addNamedRange(name, range)

Returns: NamedRange

Adds a NamedRange, which is a Range that has a name and ID to use for later retrieval, in the first tab or, for scripts that are bound to a document, the active tab.

### addViewer(emailAddress)

Returns: Document

Adds the given user to the list of viewers for the Document. If the user was already on the list of editors, this method has no effect.

### addViewer(user)

Returns: Document

Adds the given user to the list of viewers for the Document. If the user was already on the list of editors, this method has no effect.

### addViewers(emailAddresses)

Returns: Document

Adds the given array of users to the list of viewers for the Document. If any of the users were already on the list of editors, this method has no effect for them.

### getActiveTab()

Returns: Tab|null

Gets the user's currently active Tab in the document. A script can only access the active tab of the user who is running the script, and only if the script is bound to the document.

### getAs(contentType)

Returns: Blob

Retrieves the current Document contents as a blob of the specified type.

### getBlob()

Returns: Blob

Retrieves the current Document contents as a blob.

### getBody()

Returns: Body

Retrieves the first tab's Body or, for scripts that are bound to a document, the active tab's DocumentBodySection.

### getBookmark(id)

Returns: Bookmark|null

Gets the Bookmark with the given ID in the first tab or, for scripts that are bound to a document, the active tab.

### getBookmarks()

Returns: Bookmark[]

Gets all Bookmark objects in the first tab or, for scripts that are bound to a document, the active tab.

### getCursor()

Returns: Position|null

Gets the user's cursor in the active tab.

### getEditors()

Returns: User[]

Gets the list of editors for this Document.

### getFooter()

Returns: FooterSection|null

Retrieves the first tab's footer section or, for scripts that are bound to a document, the active tab's footer section.

### getFootnotes()

Returns: Footnote[]

Retrieves all the Footnote elements in the first tab's body or, for scripts that are bound to a document, the active tab's body.

### getHeader()

Returns: HeaderSection|null

Retrieves the first tab's header section or, for scripts that are bound to a document, the active tab's header section.

### getId()

Returns: String

Retrieves the document's unique identifier.

### getLanguage()

Returns: String|null

Gets the document's language code.

### getName()

Returns: String

Retrieves the title of the document.

### getNamedRangeById(id)

Returns: NamedRange|null

Gets the NamedRange with the given ID in the first tab or, for scripts that are bound to a document, the active tab.

### getNamedRanges()

Returns: NamedRange[]

Gets all NamedRange objects in the first tab or, for scripts that are bound to a document, the active tab.

### getNamedRanges(name)

Returns: NamedRange[]

Gets all NamedRange objects with the given name in the first tab or, for scripts that are bound to a document, the active tab.

### getSelection()

Returns: Range|null

Gets the user's selection in the active tab.

### getSupportedLanguageCodes()

Returns: String[]

Gets all language codes that are supported in Google Docs files.

### getTab(tabId)

Returns: Tab|null

Gets the Tab with the specified ID.

### getTabs()

Returns: Tab[]

Gets all unnested Tabs that are part of the document.

### getUrl()

Returns: String

Retrieves the URL to access the current document.

### getViewers()

Returns: User[]

Gets the list of viewers and commenters for this Document.

### newPosition(element, offset)

Returns: Position

Creates a new Position, which is a reference to a location in the tab, relative to a specific element in the first tab or, for scripts that are bound to a document, the active tab.

### newRange()

Returns: RangeBuilder

Creates a builder used to construct Range objects from tab elements in the first tab or, for scripts that are bound to a document, the active tab.

### removeEditor(emailAddress)

Returns: Document

Removes the given user from the list of editors for the Document.

### removeEditor(user)

Returns: Document

Removes the given user from the list of editors for the Document.

### removeViewer(emailAddress)

Returns: Document

Removes the given user from the list of viewers and commenters for the Document.

### removeViewer(user)

Returns: Document

Removes the given user from the list of viewers and commenters for the Document.

### saveAndClose()

Returns: void

Saves the current Document.

### setActiveTab(tabId)

Returns: void

Sets the user's selected Tab in the current document to the tab with the specified ID.

### setCursor(position)

Returns: Document

Sets the user's cursor, given a Position.

### setLanguage(languageCode)

Returns: Document

Sets the document's language code.

### setName(name)

Returns: Document

Sets the document title.

### setSelection(range)

Returns: Document

Sets the user's selection in the active tab, given a Range.
