# Extend Google Docs

## Page Summary

- Google Apps Script can create and modify Google Docs and customize their user interface.
- Apps Script can interact with Google Docs by either creating or modifying a document with appropriate permissions or by being bound to a document for special UI abilities.
- The `replaceText()` method in Apps Script is a simple way to replace text in a Google Doc and supports regular expressions.
- Custom menus, dialog boxes, and sidebars can be added to Google Docs using Apps Script, but the script must be bound to the document.
- Scripts for Google Docs can be published as add-ons to share them with other users.

Google Apps Script lets you programmatically create and modify
Docs, as well as customize the user interface with new menus,
dialog boxes, and sidebars.

## The basics

Apps Script can interact with Docs in two broad
ways: any script can create or modify a document if the script's user has
appropriate permissions for the document, and a script can also be
[bound](https://developers.google.com/apps-script/scripts_containers) to a document, which gives
the script special abilities to alter the user interface or respond when the
document is opened. To create a container-bound script from within
Docs, click **Extensions**
> **Apps Script**.

In either case, you can interact with a Docs document by using
Apps Script's [Document Service](https://developers.google.com/apps-script/reference/document),
as the following example demonstrates.

```javascript
function createDoc() {
  var doc = DocumentApp.create('Sample Document');
  var documentTab = doc.getTab('t.0').asDocumentTab();
  var body = documentTab.getBody();
  var rowsData = [['Plants', 'Animals'], ['Ficus', 'Goat'], ['Basil', 'Cat'], ['Moss', 'Frog']];
  body.insertParagraph(0, doc.getName())
      .setHeading(DocumentApp.ParagraphHeading.HEADING1);
  table = body.appendTable(rowsData);
  table.getRow(0).editAsText().setBold(true);
}
```

The preceding script creates a new document in the user's Google Drive, then
retrieves the tab with ID `t.0` (the default first tab), inserts a paragraph
that contains the same text as the document's name, styles that paragraph as a
heading, and appends a table based on the values in a two-dimensional array. The
script could also make these changes to an existing document by
replacing the call to [`DocumentApp.create`](https://developers.google.com/apps-script/reference/document/document-app#create(String))
with [`DocumentApp.openById`](https://developers.google.com/apps-script/reference/document/document-app#openById(String))
or [`openByUrl`](https://developers.google.com/apps-script/reference/document/document-app#openByUrl(String)).
For scripts created inside a document (container-bound), use
[`DocumentApp.getActiveDocument`](https://developers.google.com/apps-script/reference/document/document-app#getActiveDocument())
and [`Document.getActiveTab`](https://developers.google.com/apps-script/reference/document/document#getActiveTab()).

## Structure of a document

From Apps Script's perspective, a Docs document is
structured much like an HTML document—that is, a document is composed of one or
more [`Tab`](https://developers.google.com/apps-script/reference/document/tab) objects, each of which contain
elements (like a [`Paragraph`](https://developers.google.com/apps-script/reference/document/paragraph) or
[`Table`](https://developers.google.com/apps-script/reference/document/table)) that often contain other
elements. Most scripts that modify a Docs document begin with a
call to [`getTab`](https://developers.google.com/apps-script/reference/document/document#getTab(String))
and [`asDocumentTab`](https://developers.google.com/apps-script/reference/document/tab#asDocumentTab())
followed by [`getBody`](https://developers.google.com/apps-script/reference/document/document#getBody()),
because the [`Body`](https://developers.google.com/apps-script/reference/document/body) is a core element
that contains all other elements in a tab except for the
[`HeaderSection`](https://developers.google.com/apps-script/reference/document/header-section),
[`FooterSection`](https://developers.google.com/apps-script/reference/document/footer-section), and any
[`Footnotes`](https://developers.google.com/apps-script/reference/document/footnote).

However, there are rules about which types of elements can contain other types.
Furthermore, the Document Service in Apps Script can only insert
certain types of elements into other elements. The following tree shows which
elements can be contained by a certain type of element.

Elements shown in bold can be inserted; non-bold elements can only be
manipulated in place.

- [Document
[Tab
[DocumentTab
[Body
[**ListItem**](https://developers.google.com/apps-script/reference/document/list-item)
[Equation
[EquationFunction
[EquationFunction](https://developers.google.com/apps-script/reference/document/equation-function)...
[EquationFunctionArgumentSeparator](https://developers.google.com/apps-script/reference/document/equation-function-argument-separator)
[EquationSymbol](https://developers.google.com/apps-script/reference/document/equation-symbol)
[Text](https://developers.google.com/apps-script/reference/document/text)](https://developers.google.com/apps-script/reference/document/equation-function)
[EquationSymbol](https://developers.google.com/apps-script/reference/document/equation-symbol)
[Text](https://developers.google.com/apps-script/reference/document/text)](https://developers.google.com/apps-script/reference/document/equation)
[Footnote](https://developers.google.com/apps-script/reference/document/footnote)
[**HorizontalRule**](https://developers.google.com/apps-script/reference/document/horizontal-rule)
[InlineDrawing](https://developers.google.com/apps-script/reference/document/inline-drawing)
[**InlineImage**](https://developers.google.com/apps-script/reference/document/inline-image)
[**PageBreak**](https://developers.google.com/apps-script/reference/document/page-break)
[**Text**](https://developers.google.com/apps-script/reference/document/text)
[**Paragraph**
[Equation
[EquationFunction
[EquationFunction](https://developers.google.com/apps-script/reference/document/equation-function)...
[EquationFunctionArgumentSeparator](https://developers.google.com/apps-script/reference/document/equation-function-argument-separator)
[EquationSymbol](https://developers.google.com/apps-script/reference/document/equation-symbol)
[Text](https://developers.google.com/apps-script/reference/document/text)](https://developers.google.com/apps-script/reference/document/equation-function)
[EquationSymbol](https://developers.google.com/apps-script/reference/document/equation-symbol)
[Text](https://developers.google.com/apps-script/reference/document/text)](https://developers.google.com/apps-script/reference/document/equation)
[Footnote](https://developers.google.com/apps-script/reference/document/footnote)
[**HorizontalRule**](https://developers.google.com/apps-script/reference/document/horizontal-rule)
[InlineDrawing](https://developers.google.com/apps-script/reference/document/inline-drawing)
[**InlineImage**](https://developers.google.com/apps-script/reference/document/inline-image)
[**PageBreak**](https://developers.google.com/apps-script/reference/document/page-break)
[**Text**](https://developers.google.com/apps-script/reference/document/text)](https://developers.google.com/apps-script/reference/document/paragraph)
[**Table**
[**TableRow**
[**TableCell**
[**Paragraph**](https://developers.google.com/apps-script/reference/document/paragraph)...
[**ListItem**](https://developers.google.com/apps-script/reference/document/list-item)...
[**Table**](https://developers.google.com/apps-script/reference/document/table)...](https://developers.google.com/apps-script/reference/document/table-cell)](https://developers.google.com/apps-script/reference/document/table-row)](https://developers.google.com/apps-script/reference/document/table)
[TableOfContents
[Paragraph](https://developers.google.com/apps-script/reference/document/paragraph)...
[ListItem](https://developers.google.com/apps-script/reference/document/list-item)...
[Table](https://developers.google.com/apps-script/reference/document/table)...](https://developers.google.com/apps-script/reference/document/table-of-contents)](https://developers.google.com/apps-script/reference/document/body)
[HeaderSection
[**ListItem**
[**HorizontalRule**](https://developers.google.com/apps-script/reference/document/horizontal-rule)
[InlineDrawing](https://developers.google.com/apps-script/reference/document/inline-drawing)
[**InlineImage**](https://developers.google.com/apps-script/reference/document/inline-image)
[**Text**](https://developers.google.com/apps-script/reference/document/text)
[UnsupportedElement](https://developers.google.com/apps-script/reference/document/unsupported-element) (page number, etc.)](https://developers.google.com/apps-script/reference/document/list-item)
[**Paragraph**
[**HorizontalRule**](https://developers.google.com/apps-script/reference/document/horizontal-rule)
[InlineDrawing](https://developers.google.com/apps-script/reference/document/inline-drawing)
[**InlineImage**](https://developers.google.com/apps-script/reference/document/inline-image)
[**Text**](https://developers.google.com/apps-script/reference/document/text)
[UnsupportedElement](https://developers.google.com/apps-script/reference/document/unsupported-element) (page number, etc.)](https://developers.google.com/apps-script/reference/document/paragraph)
[**Table**
[**TableRow**
[**TableCell**
[**Paragraph**](https://developers.google.com/apps-script/reference/document/paragraph)...
[**ListItem**](https://developers.google.com/apps-script/reference/document/list-item)...
[**Table**](https://developers.google.com/apps-script/reference/document/table)...](https://developers.google.com/apps-script/reference/document/table-cell)](https://developers.google.com/apps-script/reference/document/table-row)](https://developers.google.com/apps-script/reference/document/table)](https://developers.google.com/apps-script/reference/document/header-section)
[FooterSection
[**ListItem**
[**HorizontalRule**](https://developers.google.com/apps-script/reference/document/horizontal-rule)
[InlineDrawing](https://developers.google.com/apps-script/reference/document/inline-drawing)
[**InlineImage**](https://developers.google.com/apps-script/reference/document/inline-image)
[**Text**](https://developers.google.com/apps-script/reference/document/text)
[UnsupportedElement](https://developers.google.com/apps-script/reference/document/unsupported-element) (page number, etc.)](https://developers.google.com/apps-script/reference/document/list-item)
[**Paragraph**
[**HorizontalRule**](https://developers.google.com/apps-script/reference/document/horizontal-rule)
[InlineDrawing](https://developers.google.com/apps-script/reference/document/inline-drawing)
[**InlineImage**](https://developers.google.com/apps-script/reference/document/inline-image)
[**Text**](https://developers.google.com/apps-script/reference/document/text)
[UnsupportedElement](https://developers.google.com/apps-script/reference/document/unsupported-element) (page number, etc.)](https://developers.google.com/apps-script/reference/document/paragraph)
[**Table**](https://developers.google.com/apps-script/reference/document/table)
[**TableRow**
[**TableCell**
[**Paragraph**](https://developers.google.com/apps-script/reference/document/paragraph)...
[**ListItem**](https://developers.google.com/apps-script/reference/document/list-item)...
[**Table**](https://developers.google.com/apps-script/reference/document/table)...](https://developers.google.com/apps-script/reference/document/table-cell)](https://developers.google.com/apps-script/reference/document/table-row)](https://developers.google.com/apps-script/reference/document/footer-section)
[FootnoteSection
[ListItem
[**HorizontalRule**](https://developers.google.com/apps-script/reference/document/horizontal-rule)
[**Text**](https://developers.google.com/apps-script/reference/document/text)](https://developers.google.com/apps-script/reference/document/list-item)
[**Paragraph**
[**HorizontalRule**](https://developers.google.com/apps-script/reference/document/horizontal-rule)
[**Text**](https://developers.google.com/apps-script/reference/document/text)](https://developers.google.com/apps-script/reference/document/paragraph)](https://developers.google.com/apps-script/reference/document/footnote-section)](https://developers.google.com/apps-script/reference/document/document-tab)](https://developers.google.com/apps-script/reference/document/tab)](https://developers.google.com/apps-script/reference/document/document)

## Replace text

Apps Script is often used to replace text in Docs.
Suppose you have a spreadsheet full of client information and you want to
generate a personalized Docs for each client. (This type of
operation is often called a mail merge.)

You can replace text using the [`replaceText`](https://developers.google.com/apps-script/reference/document/body#replaceText(String,String))
method, which supports most JavaScript
[regular expression](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/RegExp)
features. In the following example, the first function adds placeholder text to
the document, and the second replaces that text with properties from a `client`
object.

Both of these functions use the
[`getActiveDocument`](https://developers.google.com/apps-script/reference/document/document-app#getActiveDocument())
and
[`getActiveTab`](https://developers.google.com/apps-script/reference/document/document#getActiveTab())
methods, which only apply to scripts created inside a Docs
document; in a stand-alone script, use
[`DocumentApp.create`](https://developers.google.com/apps-script/reference/document/document-app#create(String)),
[`openById`](https://developers.google.com/apps-script/reference/document/document-app#openById(String)),
or [`openByUrl`](https://developers.google.com/apps-script/reference/document/document-app#openByUrl(String)),
combined with [`Document.getTab`](https://developers.google.com/apps-script/reference/document/document#getTab(String)),
instead.

**Add some placeholders**

```javascript
function createPlaceholders() {
  var body = DocumentApp.getActiveDocument().getActiveTab().asDocumentTab().getBody();
  body.appendParagraph('{name}');
  body.appendParagraph('{address}');
  body.appendParagraph('{city} {state} {zip}');
}
```

**Replace the placeholders**

```javascript
function searchAndReplace() {
  var body = DocumentApp.getActiveDocument().getActiveTab().asDocumentTab().getBody();
  var client = {
    name: 'Joe Script-Guru',
    address: '100 Script Rd',
    city: 'Scriptville',
    state: 'GA',
    zip: 94043
  };

  body.replaceText('{name}', client.name);
  body.replaceText('{address}', client.address);
  body.replaceText('{city}', client.city);
  body.replaceText('{state}', client.state);
  body.replaceText('{zip}', client.zip);
}
```

## Custom menus and user interfaces

You can customize Docs by adding
[custom menus](https://developers.google.com/apps-script/guides/menus),
[dialog boxes, and sidebars](https://developers.google.com/apps-script/guides/dialogs). Keep in mind that a
script can only interact with the UI of the document it is
[bound](https://developers.google.com/apps-script/scripts_containers) to.

To learn more about creating custom interfaces with HTML and CSS, see the
[guide to HTML Service](https://developers.google.com/apps-script/guides/html-service#serve_html_as_a_google_docs_sheets_or_forms_user_interface).
If you plan to publish your interface as an
[add-on](https://developers.google.com/workspace/add-ons/overview), follow the
[style guide](https://developers.google.com/workspace/add-ons/guides/editor-style) to ensure its appearance
is consistent with the Docs editor.

## Add-ons for Docs

[Add-ons](https://developers.google.com/workspace/add-ons/overview) run inside
Docs and can be installed from the Docs
add-on store. If you've developed a script for
Docs and want to share it with the world,
Apps Script lets you
[publish](https://developers.google.com/workspace/add-ons/how-tos/editor-publish-overview) your script as an
add-on so other users can install it from the
add-on store.

To create an add-on for Docs, see the
[quickstart for building Docs
add-ons](https://developers.google.com/workspace/add-ons/editors/docs/quickstart/translate).

## Triggers

Scripts that are [bound](https://developers.google.com/apps-script/scripts_containers) to a Google
Doc can use a [simple trigger](https://developers.google.com/apps-script/understanding_triggers) to respond
to the document's `onOpen` [event](https://developers.google.com/apps-script/understanding_events), which
occurs whenever a user who has edit access to the document opens it in
Docs.

To set up the trigger, write a function called `onOpen`. For an example
of this trigger, see [Custom menus in Google Workspace](https://developers.google.com/apps-script/guides/menus).
Although the trigger is useful for adding menus, it cannot use any Apps
Script services that require authorization.
