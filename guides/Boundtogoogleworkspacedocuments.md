# Container-bound Scripts

[Video](https://www.youtube.com/watch?v=BK9sWR0I6Ys)

A script is bound to a Google Sheets, Google Docs,
Google Slides, or Google Forms file if it was created from that document
rather than as a [standalone script](https://developers.google.com/apps-script/guides/standalone). The file
that a bound script is attached to is called a "container." Bound scripts
generally behave like standalone scripts except that they don't appear in
Google Drive, they can't be detached from the file they are bound to, and
they gain a few special privileges over the parent file.

Scripts can also be bound to Google Sites, but these scripts are almost
always deployed as [web apps](https://developers.google.com/apps-script/guides/web). Scripts bound to
Sheets, Docs, Slides, or
Forms can also become web apps, although this is uncommon.

Bound scripts are effectively unpublished
[Google Workspace add-ons](https://developers.google.com/workspace/add-ons/concepts/types#editor_add-ons) that
function only for the file they are bound to.

## Create a bound script

You can create bound scripts in Docs, Sheets,
Slides, and Forms.

### Docs, Sheets, or Slides

To create a bound script in Docs, Sheets, or
Slides, open a document in Docs, a spreadsheet in
Sheets, or a presentation in Slides and click
**Extensions** \>
**Apps Script** . To reopen the script in the future, do the same
thing or open the script from the [Apps Script
dashboard](https://script.google.com/home).

### Forms

To create a bound script in Forms, open a form and click
**More**
\> **Script editor** . To reopen the script in
the future, do the same thing or open the script from the
[Apps Script dashboard](https://script.google.com/home).

The [`clasp`](https://developers.google.com/apps-script/guides/clasp) tool can't create bound scripts, but it
can clone and edit them.

## Special methods

Bound scripts can call a few methods that standalone scripts can't:

- [`getActiveSpreadsheet`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#getActiveSpreadsheet()), [`getActiveDocument`](https://developers.google.com/apps-script/reference/document/document-app#getActiveDocument()), [`getActivePresentation`](https://developers.google.com/apps-script/reference/slides/slides-app#getactivepresentation), and [`getActiveForm`](https://developers.google.com/apps-script/reference/forms/form-app#getActiveForm()) allow bound scripts to refer to their parent file without referring to the file's ID.
- [`getUi`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#getUi()) lets bound scripts access the user interface for their parent file to add [custom
  menus, dialogs, and sidebars](https://developers.google.com/apps-script/guides/bound#custom_menus_dialogs_and_sidebars).
- In Sheets, [`getActiveSheet`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#getActiveSheet()), [`getActiveRange`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#getActiveRange()), and [`getActiveCell`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#getActiveCell()) let the script determine the user's current sheet, selected range of cells, or selected individual cell. [`setActiveSheet`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#setActiveSheet(Sheet)) and [`setActiveRange`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#setActiveRange(Range)) let the script change those selections.
- In Docs, [`getActiveTab`](https://developers.google.com/apps-script/reference/document/document#getActiveTab()), [`getCursor`](https://developers.google.com/apps-script/reference/document/document#getCursor()), and [`getSelection`](https://developers.google.com/apps-script/reference/document/document#getSelection()) let the script determine the user's current tab, position of the user's cursor, or selected text. [`setActiveTab`](https://developers.google.com/apps-script/reference/document/document#setActiveTab(String)), [`setCursor`](https://developers.google.com/apps-script/reference/document/document#setCursor(Position)) and [`setSelection`](https://developers.google.com/apps-script/reference/document/document#setSelection(Range)) let the script change those selections.

For more information, see the [guide to extending
Sheets](https://developers.google.com/apps-script/guides/sheets) or the [guide to extending
Docs](https://developers.google.com/apps-script/guides/docs).

These methods are only available to bound scripts run from the script editor,
menu items, dialogs, sidebars, or triggers. When a bound script is run as a web
app or using the [Google Apps Script API](https://developers.google.com/apps-script/api/how-tos/execute), these
methods aren't available.

## Custom menus, dialogs, and sidebars

Bound scripts can customize Sheets, Docs, and
Forms by adding [custom menus](https://developers.google.com/apps-script/guides/menus) and
[dialog boxes or sidebars](https://developers.google.com/apps-script/guides/dialogs). A script can only
interact with the user interface for the current instance of an open file.
A script bound to one document can't affect the user interface of another
document.

> [!NOTE]
> Add-ons can also add custom menus, dialogs and sidebars. It is recommended to develop add-ons using [standalone scripts](https://developers.google.com/apps-script/guides/standalone).

## Triggers

Bound scripts can use [simple triggers](https://developers.google.com/apps-script/guides/triggers) like the
special `onOpen` function, which runs automatically whenever a file is opened
by a user who has edit access. Like all types of scripts, they can also use
[installable triggers](https://developers.google.com/apps-script/guides/triggers/installable).

## Custom functions

A [custom function](https://developers.google.com/apps-script/guides/sheets/functions) is a function in a
script bound to Sheets that you call directly from a cell using
the syntax `=myFunctionName()`. Custom functions are similar to the hundreds of
[built-in functions](https://support.google.com/drive/topic/1361471) in
Sheets like
[`AVERAGE`](https://support.google.com/drive/answer/3093615) or
[`SUM`](https://support.google.com/drive/answer/3093669) except that you define
the custom function's behavior.

## Access to bound scripts

Only users who have permission to edit a container can run its bound script.
Collaborators who have only view access can't open the script editor. If they
make a copy of the container file, they become the owner of the copy and can see
and run a copy of the script.

To learn how to share a script's container file, refer to [Share files from
Drive](https://support.google.com/drive/answer/2494822).

All container-bound scripts use the same owner, viewer, and
editor access list defined for the container file. The container owner takes
ownership of a new script project regardless of who created it.