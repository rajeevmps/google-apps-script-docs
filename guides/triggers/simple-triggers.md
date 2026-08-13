# Simple Triggers

## Page Summary

- Simple triggers in Apps Script are reserved functions that run automatically on specific events like opening or editing a document.
- Installable triggers offer more features than simple triggers but require activation.
- Both simple and installable triggers pass an event object containing context information to the triggered function.
- Simple triggers have restrictions, including limitations on services that require authorization and a maximum execution time of 30 seconds.

Triggers let Google Apps Script run a function automatically when a
certain event, like opening a document, occurs. Simple triggers are a set
of reserved functions built into Apps Script, like the function
`onOpen(e)`, which executes when a user opens a Google Docs,
Sheets, Slides, or Forms file.
[Installable triggers](https://developers.google.com/apps-script/guides/triggers/installable) offer more
capabilities than simple triggers but must be activated before use. For both
types of triggers, Apps Script passes the triggered function an
[event object](https://developers.google.com/apps-script/guides/triggers/events) that contains information
about the context in which the event occurred.

For information on how to use triggers in Google Workspace add-on
projects, see [Triggers for Google Workspace add-ons](https://developers.google.com/workspace/add-ons/concepts/workspace-triggers).

## Getting started

To use a simple trigger, create a function that uses one of these
reserved function names:

- `onOpen(e)` runs when a user opens a spreadsheet, document, presentation, or
form that the user has permission to edit.
- `onInstall(e)` runs when a user installs an
[Editor add-on](https://developers.google.com/workspace/add-ons/concepts/types#editor_add-ons)
from within Google Docs, Sheets, Slides, or
Forms.
- `onEdit(e)` runs when a user changes a value in a spreadsheet.
- `onSelectionChange(e)` runs when a user changes the selection in a
spreadsheet.
- `doGet(e)` runs when a user visits a [web app](https://developers.google.com/apps-script/guides/web)
or a program sends an HTTP `GET` request to a web app.
- `doPost(e)` runs when a program sends an HTTP `POST` request to a web app.

The `e` parameter in the function names above is an
[event object](https://developers.google.com/apps-script/guides/triggers/events) that is passed to the
function. The object contains information about the context that caused the
trigger to fire, but using it is optional.

## Restrictions

Because simple triggers fire automatically, without asking the user for
authorization, they are subject to several restrictions:

- The script must be [bound](https://developers.google.com/apps-script/scripts_containers) to a Google
Sheets, Slides, Docs, or
Forms file, or else be an
[add-on](https://developers.google.com/apps-script/add-ons/concepts/workspace-triggers)
that extends one of those applications.
- They don't run if a file is opened in read-only (view or comment) mode.
- Script executions and API requests don't cause triggers to run. For example,
calling [`Range.setValue()`](https://developers.google.com/apps-script/reference/spreadsheet/range#setvaluevalue)
to edit a cell does not cause the spreadsheet's `onEdit` trigger to run.
- They can't access [services](https://developers.google.com/apps-script/guides/services) that require
[authorization](https://developers.google.com/apps-script/guides/services/authorization). For example,
a simple trigger can't send an email because the
[Gmail service](https://developers.google.com/apps-script/reference/gmail) requires
authorization, but a simple trigger can translate a phrase with the
[Language service](https://developers.google.com/apps-script/reference/language), which is anonymous.
- They can modify the file they are bound to, but can't access other files
because that would require authorization.
- They may or may not be able to determine the identity of the current user,
depending on a
[complex set of security restrictions](https://developers.google.com/apps-script/reference/base/session#getActiveUser()).
- They can't run for longer than 30 seconds.
- In certain circumstances,
[Editor add-ons](https://developers.google.com/workspace/add-ons/concepts/editor-addons) run their
`onOpen(e)` and `onEdit(e)` simple triggers in a no-authorization mode that
presents some additional complications. For more information, see the
[guide to the add-on authorization lifecycle](https://developers.google.com/workspace/add-ons/concepts/addon-authorization#editor_add-on_authorization).
- Simple triggers are subject to Apps Script trigger
[quota limits](https://developers.google.com/apps-script/guides/services/quotas).

These restrictions don't apply to `doGet(e)` or `doPost(e)`.

## `onOpen(e)`

The `onOpen(e)` trigger runs automatically when a user opens a spreadsheet,
document, presentation, or form that they have permission to edit. (The
trigger does not run when responding to a form, only when opening the form to
edit it.) `onOpen(e)` is most commonly used to add custom
[menu items](https://developers.google.com/apps-script/guides/menus) to Google Sheets,
Slides, Docs, or Forms.

```javascript
/**
 * The event handler triggered when opening the spreadsheet.
 * @param {Event} e The onOpen event.
 * @see https://developers.google.com/apps-script/guides/triggers#onopene
 */
function onOpen(e) {
  // Add a custom menu to the spreadsheet.
  SpreadsheetApp.getUi() // Or DocumentApp, SlidesApp, or FormApp.
    .createMenu("Custom Menu")
    .addItem("First item", "menuItem1")
    .addToUi();
}
```

## `onInstall(e)`

The `onInstall(e)` trigger runs automatically when a user installs an
[Editor add-on](https://developers.google.com/workspace/add-ons/concepts/types#editor_add-ons)
from within Google Docs, Sheets, Slides, or
Forms. The trigger does not run when a user
installs the add-on from the
[Google Workspace Marketplace](https://workspace.google.com/marketplace/)
website.
The most common use of `onInstall(e)` is to call `onOpen(e)` to add
custom menus. After an add-on is installed, the file
is already open, and thus `onOpen(e)` does not run on its own unless the file
is reopened.
Note that there are certain restrictions on what `onInstall(e)` can
do. Learn more about
[authorization](https://developers.google.com/workspace/add-ons/concepts/addon-authorization#installing).

```javascript
/**
 * The event handler triggered when installing the add-on.
 * @param {Event} e The onInstall event.
 * @see https://developers.google.com/apps-script/guides/triggers#oninstalle
 */
function onInstall(e) {
  onOpen(e);
}
```

## `onEdit(e)`

The `onEdit(e)` trigger runs automatically when a user changes the value of any
cell in a spreadsheet. Most `onEdit(e)` triggers use the information in the
[event object](https://developers.google.com/apps-script/guides/triggers/events) to respond appropriately.
For example, the `onEdit(e)` function below sets a comment on the cell that
records the last time it was edited.

```javascript
/**
 * The event handler triggered when editing the spreadsheet.
 * @param {Event} e The onEdit event.
 * @see https://developers.google.com/apps-script/guides/triggers#onedite
 */
function onEdit(e) {
  // Set a comment on the edited cell to indicate when it was changed.
  const range = e.range;
  range.setNote(`Last modified: ${new Date()}`);
}
```

The `onEdit()` trigger only queues up to 2 trigger events.

## `onSelectionChange(e)`

The `onSelectionChange(e)` trigger runs automatically when a user changes the
selection in a spreadsheet. To activate this trigger, refresh the
spreadsheet once the trigger is added and every time the spreadsheet is opened.

If the selection moves between multiple cells in a short time, some selection
change events might be skipped to reduce latency. For example, if many selection
changes are made within two seconds of each other, only the first and last
selection changes activate the `onSelectionChange(e)` trigger.

In the following example, if an empty cell is selected, the
`onSelectionChange(e)` function sets the cell's background to red.

```javascript
/**
 * The event handler triggered when the selection changes in the spreadsheet.
 * @param {Event} e The onSelectionChange event.
 * @see https://developers.google.com/apps-script/guides/triggers#onselectionchangee
 */
function onSelectionChange(e) {
  // Set background to red if a single empty cell is selected.
  const range = e.range;
  if (
    range.getNumRows() === 1 &&
    range.getNumColumns() === 1 &&
    range.getCell(1, 1).getValue() === ""
  ) {
    range.setBackground("red");
  }
}
```

## `doGet(e)` and `doPost(e)`

The `doGet(e)` trigger runs automatically when a user visits a
[web app](https://developers.google.com/apps-script/guides/web) or a program sends an HTTP `GET` request
to a web app. `doPost(e)` runs when a program sends an HTTP `POST` request to a
web app. These triggers are demonstrated more in the guides to
[web apps](https://developers.google.com/apps-script/guides/web), [HTML service](https://developers.google.com/apps-script/guides/html),
and [Content service](https://developers.google.com/apps-script/guides/content). Note that `doGet(e)` and
`doPost(e)` are not subject to the restrictions listed above.

## Available types of triggers

If the restrictions on simple triggers keep them from meeting
your needs, an [installable trigger](https://developers.google.com/apps-script/guides/triggers/installable)
might work instead. The table below summarizes which types of triggers are
available for each type of event. For example, Google Sheets,
Slides, Forms, and Docs all support
simple open triggers, but only Sheets, Docs and
Forms support installable open triggers.

| Event | Simple triggers | Installable triggers |
|---|---|---|
| Open | Sheets Slides Forms* Docs `function onOpen(e)` | Sheets Forms* Docs |
| Edit | Sheets `function onEdit(e)` | Sheets |
| Selection change | Sheets `function onSelectionChange(e)` |  |
| Install | Sheets Slides Forms Docs `function onInstall(e)` |  |
| Change |  | Sheets |
| Form submit |  | Sheets Forms |
| Time-driven (clock) |  | Sheets Slides Forms Docs Standalone |
| Get | Standalone `function doGet(e)` |  |
| Post | Standalone `function doPost(e)` |  |

* The open event for Google Forms does not occur when a user opens a
form to respond, but rather when an editor opens the form to modify it.
