# Custom menus for Editor add-ons

Published [Editor add-ons](/workspace/add-ons/concepts/types#editor_add-ons) can create custom menu items under their editor's **Extensions** menu. Insert an add-on menu using `Ui.createAddonMenu` and add items to it with `Menu.addItem`. Menus are usually created in the add-on's `onOpen` method.

> **Caution:** Unpublished add-ons can also [create custom top-level menus](/apps-script/guides/menus#custom_menus_in_google_docs_sheets_slides_or_forms), but these move under the **add-ons** menu if the add-on is published, which might result in an unintended user experience. If you intend to publish the add-on, always use [`Ui.createAddonMenu`](/apps-script/reference/base/ui#createAddonMenu()) to define the add-on menu.

Create dynamic menus that change based on user interactions or add-on state. However, add-ons must create an initial menu *before* the add-on is authorized by the user. Because of this, check the add-on's [authorization mode](/workspace/add-ons/concepts/editor-auth-lifecycle#authorization_modes) prior to constructing menus in `onOpen`. Don't take any action that requires authorization (such as checking script [`Properties`](/apps-script/reference/properties)) while the add-on is in `ScriptApp.AuthMode.NONE`. See the [authorization lifecycle](/workspace/add-ons/concepts/editor-auth-lifecycle#the_complete_lifecycle) for more details on the authorization modes and lifecycle.

Attempting to take actions that require authorization when the authorization mode is `ScriptApp.AuthMode.NONE` results in an error. This might prevent your add-on menus from being displayed.

The following example shows how to build a dynamic add-on menu for different authorization modes:

```
function onOpen(e) {
  // Or DocumentApp, SlidesApp, or FormApp.
  var menu = SpreadsheetApp.getUi().createAddonMenu();
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
    // Record analytics.
    UrlFetchApp.fetch('http://www.example.com/analytics?event=open');
  }
  menu.addToUi();
}
```
