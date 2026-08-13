# Built-in Google Services

Google Apps Script provides more than 30 built-in services for interacting
with user data, other Google systems, and external systems. These services are
provided as global objects akin to JavaScript's standard
[`Math`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math)
object. For example, just as `Math` offers methods like `random()` and constants
like `PI`, Apps Script's [Spreadsheet
service](https://developers.google.com/apps-script/reference/spreadsheet) offers methods like
[`openById(id)`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#openById(String)),
classes (child objects) like
[`Range`](https://developers.google.com/apps-script/reference/spreadsheet/range), and enums like
[`DataValidationCriteria`](https://developers.google.com/apps-script/reference/spreadsheet/data-validation-criteria).

The reference documentation for services that control Google Workspace
products are collected in the "Google Workspace Services" section under
the "Reference" header in the sidebar of this site. Utility services (for things
like creating user interfaces, parsing XML, or writing log data) are collected
in the "Script Services" section.

## Modern JavaScript features

Apps Script supports two JavaScript runtimes: the modern
[**V8**](https://v8.dev/) runtime and an older one powered by Mozilla's
[**Rhino JavaScript interpreter**](https://en.wikipedia.org/wiki/Rhino_(JavaScript_engine)).

The [V8 runtime](https://developers.google.com/apps-script/guides/v8-runtime) supports modern
[ECMAScript](https://en.wikipedia.org/wiki/ECMAScript) syntax and features.
The Rhino runtime is based on the older
[JavaScript 1.6](https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/1.6)
standard, plus a few features from
[1.7](https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/1.7) and
[1.8](https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/1.8).
[Choose which runtime](https://developers.google.com/apps-script/guides/v8-runtime#enabling_the_v8_runtime)
to use with your script, but the V8 runtime is strongly recommended.

Each runtime supports JavaScript classes and objects that are available to your
script in addition to the built-in
and [advanced Google services](https://developers.google.com/apps-script/guides/services/advanced). Your
scripts can use common objects like
[`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array),
[`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date),
[`RegExp`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp),
[and so forth](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference),
as well as the
[`Math`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math) and
[`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
global objects.

Because Apps Script code runs on Google's servers (with the
exception of [HTML-service](https://developers.google.com/apps-script/guides/html) pages),
browser-based JavaScript features like DOM manipulation or the
[`Window`](https://developer.mozilla.org/en-US/docs/Web/API/Window) API are not
available in Apps Script.

## Autocomplete

The script editor provides a "content assist" feature, more commonly called
"autocomplete," which reveals the global objects as well as methods and enums
that are valid in the script's current context. Autocomplete suggestions appear
automatically whenever you type a period after a global object, enum, or method
call that returns an Apps Script class. For example:

- If you type the full name of a global object or select one from autocomplete, then type `.` (a period), you see all methods and enums for that class.
- If you type a few characters, you see all valid suggestions that begin with those characters.

## Global objects

Each service provides at least one global (top-level) object; for example, the
[Gmail service](https://developers.google.com/apps-script/reference/gmail) is accessed solely from
the [`GmailApp`](https://developers.google.com/apps-script/reference/gmail/gmail-app) object. Some services
provide multiple global objects; for example, the
[Base service](https://developers.google.com/apps-script/reference/base) includes four global objects:
[`Browser`](https://developers.google.com/apps-script/reference/base/browser),
[`Logger`](https://developers.google.com/apps-script/reference/base/logger),
[`MimeType`](https://developers.google.com/apps-script/reference/base/mime-type), and
[`Session`](https://developers.google.com/apps-script/reference/base/session).

## Methods

The global objects of nearly all built-in or
[advanced services](https://developers.google.com/apps-script/guides/services/advanced) include methods that
return data or an Apps Script class. Scripts make method calls in
this format:

    GlobalObjectName.methodName(argument1, argument2, ..., argumentN);

For example, a script can send an email by calling the
[`sendEmail(recipient, subject, body)`](https://developers.google.com/apps-script/reference/gmail/gmail-app#sendEmail(String,String,String))
method of the Gmail service like so:

    GmailApp.sendEmail('claire@example.com', 'Subject line', 'This is the body.');

If a method returns another Apps Script class, chain method
calls on one line. (Return types are shown both in autocomplete and in a
method's reference documentation.) For example, the method
[`DocumentApp.create()`](https://developers.google.com/apps-script/reference/document/document-app#create(String))
returns a [`Document`](https://developers.google.com/apps-script/reference/document/document); thus, the
following two sections of code are equivalent:

    var doc = DocumentApp.create('New document');
    var body = doc.getTab('t.0').asDocumentTab().getBody();
    body.appendParagraph('New paragraph.');

    // Same result as above.
    DocumentApp.create('New document').getTab('t.0').asDocumentTab().getBody()
        .appendParagraph('New paragraph.');

## Child classes

Every service includes one or more child classes that you can't access
from the top level as a global object. You also can't use the `new` keyword to
construct these classes, as you would with standard JavaScript classes like
[`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date).
To access a child class, you must call a method that returns it. If you're
not sure how to access a certain class, visit the root page for the service's
reference documentation---it lists the classes for the service, and the methods
that return them.

## Interfaces

Some services include classes labeled as "interfaces" in the reference
documentation. These are generic classes used as return types for methods that
can't determine the precise type in advance. For example, the
[Document service](https://developers.google.com/apps-script/reference/document) method
[`Body.getChild(childIndex)`](https://developers.google.com/apps-script/reference/document/body#getChild(Integer))
returns a generic [`Element`](https://developers.google.com/apps-script/reference/document/element) object.
The `Element` interface represents some other class, possibly a
[`Paragraph`](https://developers.google.com/apps-script/reference/document/paragraph) or
[`Table`](https://developers.google.com/apps-script/reference/document/table). Interface objects are rarely
useful on their own; instead, call a method like
[`Element.asParagraph()`](https://developers.google.com/apps-script/reference/document/element#asParagraph())
to cast the object back to a specific class.

## Enums

Most services include enums (enumerated types) of named values. For
example, the [Google Drive service](https://developers.google.com/apps-script/reference/drive) uses the
enums [`Access`](https://developers.google.com/apps-script/reference/drive/access) and
[`Permission`](https://developers.google.com/apps-script/reference/drive/permission) to determine which users
have access to a file or folder. In most cases, you access these enums from
the global object, as shown in the following example:

    // Creates a folder that anyone on the Internet can read from and write to.
    // (Domain administrators can prohibit this setting for Google Workspace users.)
    var folder = DriveApp.createFolder('Shared Folder');
    folder.setSharing(DriveApp.Access.ANYONE, DriveApp.Permission.EDIT);