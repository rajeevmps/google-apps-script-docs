# Editor add-on authorization

Authorization for many Google Apps Script apps is straightforward. The script project asks for any missing permissions it needs when someone attempts to use it.

The authorization model for [Editor add-ons](/workspace/add-ons/concepts/types#editor_add-ons) is more complex for several reasons:

- When a user creates a file, all the add-ons the user installs are listed in the **Extensions** menu, even if the user hasn't authorized those add-ons yet.
- These add-ons work on files in Google Drive that can be shared with collaborators. Collaborators who don't have the Editor add-on installed see it in documents where the file creator used it.
- Editor add-ons automatically run their `onOpen` functions when a document opens.

To protect user data, authorization modes are applied that make some services unavailable to `onOpen`. This guide explains what your code can do and when.

## Authorization model

The authorization mode of an Editor add-on depends on its state, which depends on who is using it: the user who installed the add-on or a collaborator.

### Editor add-on states

Editor add-ons in the **Extensions** menu are installed, enabled, or both:

- An add-on is *installed* for a particular user after they or their administrator get it from the Google Workspace Marketplace and authorize it to access their Google data.
- An add-on is *enabled* in a document, form, presentation, or spreadsheet when anyone uses it there.
- When people collaborate on a file and one of them uses an add-on, it's *installed* for that user and *enabled* for the file.

The following table summarizes the differences between installed and enabled. When you [test a script as an add-on](/workspace/add-ons/how-tos/testing-editor-addons), you can run the test in either or both states.

|  | Installed | Enabled |
| --- | --- | --- |
| Applies to | User | Document, form, presentation, or spreadsheet |
| Caused by | Getting an add-on from the store | Getting an add-on from the store while using that document, form, presentation, or spreadsheet, or using a previously installed add-on in that document, form, presentation, or spreadsheet |
| Menu visible to | Only that user, in all documents, forms, presentations, or spreadsheets they open or create | All collaborators on that document, form, presentation, or spreadsheet |
| Authorization mode for `onOpen` | `AuthMode.NONE` (unless it's also *enabled*, in which case `AuthMode.LIMITED)` | `AuthMode.LIMITED` |

### Authorization modes

The `onOpen` function of an Editor add-on runs automatically when a user opens a document, form, presentation, or spreadsheet. To protect users' data, Apps Script restricts what the `onOpen` function can do. The Editor add-on state determines which authorization mode the `onOpen` function runs in.

If an Editor add-on is *enabled* in the file, form, presentation, or spreadsheet, `onOpen` runs in `AuthMode.LIMITED`. If the add-on isn't enabled and is only *installed*, `onOpen` runs in `AuthMode.NONE`.

In `AuthMode.NONE`, an add-on can't run certain services until the user interacts with the add-on by clicking or running custom functions. If your add-on tries to use these services in `onOpen`, `onInstall`, or global scope, **permissions fail and other calls, such as filling in menus, stop**. Help is the only supported option.

To run restricted service calls, you must use the `AuthMode.FULL` authorization mode. User interaction functions, such as clicking a menu option, run only in this mode. After the code is run in `AuthMode.FULL` mode, the add-on can use all authorized scopes.

Only [published](/workspace/add-ons/how-tos/publish-add-on-overview#published) Editor add-ons can be in `AuthMode.NONE`; [unpublished](/workspace/add-ons/how-tos/publish-add-on-overview#unpublished) Editor add-ons run `onOpen` in `AuthMode.LIMITED`. However, intended in either authorization mode. To do this, [test an Editor add-on](/workspace/add-ons/how-tos/testing-editor-addons).

Apps Script passes the authorization mode as the `authMode` property of the Apps Script [event parameter](/apps-script/understanding_events), `e`; the value of `e.authMode` corresponds to a constant in the Apps Script [`ScriptApp.AuthMode`](/apps-script/reference/script/auth-mode) enum.

Authorization modes apply to all Apps Script execution methods, including running from the script editor, from a menu item, or from an Apps Script [`google.script.run`](/apps-script/guides/html/communication) call. However, the `e.authMode` property can only be inspected if the script runs as the result of a [trigger](/workspace/add-ons/concepts/editor-triggers) such as `onOpen`, `onEdit` or `onInstall`. [Custom functions](/workspace/add-ons/editors/sheets#custom_functions) in Google Sheets use their own authorization mode, `AuthMode.CUSTOM_FUNCTION`, which is similar to `LIMITED` but has slightly different restrictions. For all other cases, scripts run in `AuthMode.FULL`, as described in the following table.

|  | `NONE` | `LIMITED` | `CUSTOM_FUNCTION` | `FULL` |
| --- | --- | --- | --- | --- |
| Occurs for | `onOpen` (if the user has installed an add-on but not enabled it in the document, form, presentation, or spreadsheet) | `onOpen` (all other times) `onEdit` (only in Sheets) | [Custom functions](/apps-script/execution_custom_functions) | All other times, including: [installable triggers](/apps-script/guides/triggers/installable) `onInstall` `google.script.run` |
| Access to user data | [Locale only](/apps-script/reference/base/session#getActiveUserLocale()) | [Locale only](/apps-script/reference/base/session#getActiveUserLocale()) | [Locale only](/apps-script/reference/base/session#getActiveUserLocale()) | Yes |
| Access to document, form, presentation, or spreadsheet | No | Yes | Yes — read-only | Yes |
| Access to user interface | [Add menu items](/workspace/add-ons/concepts/menus) | [Add menu items](/workspace/add-ons/concepts/menus) | No | Yes |
| Access to `Properties` | No | Yes | Yes | Yes |
| Access to `Jdbc`, `UrlFetch` | No | No | Yes | Yes |
| Other services | `Logger` `Utilities` | Any services that don't access user data | Any services that don't access user data | All services |

## Authorization lifecycle of an Editor add-on

When an add-on is installed for the current user or enabled in the current file, the add-on is *loaded* for the document, form, presentation, or spreadsheet when that file is opened. The add-on is listed in the **Extensions** menu and starts listening for the [simple triggers](/workspace/add-ons/concepts/editor-triggers) `onInstall`, `onOpen`, and `onEdit`. If a user clicks an **Extensions** menu item, it runs.

### The Editor add-on is installed

When an Editor add-on is installed from the store, its `onInstall` function runs in `AuthMode.FULL`. In this authorization mode, the add-on can run a complex setup routine. You should also use `onInstall` to create menu items, since the document, form, presentation, or spreadsheet is already open and your `onOpen` function hasn't run. The following sample shows how to call the `onOpen` function from the `onInstall` function:

```
function onInstall(e) {
  onOpen(e);
  // Perform additional setup as needed.
}
```

### The Editor add-on is opened

When a document, form, presentation, or spreadsheet opens, it loads every Editor add-on that the current user has installed or that any collaborator has enabled in the file, and calls each of their `onOpen` functions. The authorization mode that `onOpen` runs in depends on whether an add-on is installed or enabled.

If an add-on only creates a basic menu, the mode doesn't matter. The following sample shows a basic `onOpen` function:

```
function onOpen(e) {
  SpreadsheetApp.getUi().createAddonMenu() // Or DocumentApp.
      .addItem('Insert chart', 'insertChart')
      .addItem('Update charts', 'updateCharts')
      .addToUi();
}
```

To add dynamic menu items based on stored Apps Script [properties](/apps-script/guides/properties), to read the contents of the current file, or to perform other advanced tasks, you must identify the authorization mode and handle it appropriately.

The following sample shows an advanced `onOpen` function that changes its action based on the authorization mode:

```
function onOpen(e) {
  var menu = SpreadsheetApp.getUi().createAddonMenu(); // Or DocumentApp.
  if (e && e.authMode == ScriptApp.AuthMode.NONE) {
    // Add a normal menu item (works in all authorization modes).
    menu.addItem('Start workflow', 'startWorkflow');
  } else {
    // Add a menu item based on properties (doesn't work in AuthMode.NONE).
    var properties = PropertiesService.getDocumentProperties();
    var workflowStarted = properties.getProperty('workflowStarted');
    if (workflowStarted) {
      menu.addItem('Check workflow status', 'checkWorkflow');
    } else {
      menu.addItem('Start workflow', 'startWorkflow');
    }
  }
  menu.addToUi();
}
```

When the `onOpen` function runs, the entire script loads and global statements run under the same authorization mode as `onOpen`. If the authorization mode prohibits the global statements, both the global statements and `onOpen` fail to run. If the published add-on fails to add its menu items, review the browser console to see if an error was returned. Then, examine your script to see whether the `onOpen` function or global variables call services that aren't allowed in `AuthMode.NONE`.

Add-ons can't open sidebars or dialogs while executing in `AuthMode.LIMITED`. You can use [menu items](/workspace/add-ons/concepts/menus) to open sidebars and dialogs since these run in `AuthMode.FULL`.

### A user runs the Editor add-on

When a user clicks an **Extensions** menu item, Apps Script first checks whether the user has installed the add-on and prompts them to do so if not. If the user has authorized the add-on, the script runs the function that corresponds to the menu item in `AuthMode.FULL`. The add-on is enabled in the document, form, presentation, or spreadsheet if it wasn't already.

## Troubleshoot add-on menus not rendering

Your add-on menu might not render if your code doesn't manage the authorization modes correctly. For example:

- An add-on tries to run an Apps Script service that isn't supported by the current authorization mode.
- An add-on tries to run a service call before a user interacts with it.

To remove or rearrange a service call that's causing permission errors in `AuthMode.NONE`, try the following actions:

1. Open the Apps Script project for your add-on and locate the `onOpen` function.
2. Search the `onOpen` function for mentions of Apps Script services or objects associated with them, such as `PropertiesService`, `SpreadsheetApp` or `GmailApp`.
3. If a service is used for anything other than creating the UI elements, remove it or wrap it in a comment block. Leave only these methods: `.getUi`, `.createMenu`, `.addItem`, and `.addToUi`. Also find and remove any service that is outside a function.
4. Identify functions that could contain the lines of code commented or removed in the previous step, particularly those that use the information they produce, and move the service calls to the functions that need them. Rearrange or rewrite your codebase to accommodate the changes made in the previous steps.
5. Save the code and create a test deployment. When you create a test deployment, ensure that the **Config** field is **Installed for current user** and that the text below the Config box says **Test in `AuthMode.NONE`**.
6. Launch the test deployment and open the **Extensions** menu.
7. If all menu items are displayed, the problem is fixed. If you only see the **Help** menu, go back to step 1. You might have missed a service call.

## Related topics

- [Web Apps](/apps-script/guides/web)
- [Add-on types](/workspace/add-ons/concepts/types)
- [Test an Editor add-on](/workspace/add-ons/how-tos/testing-editor-addons)
