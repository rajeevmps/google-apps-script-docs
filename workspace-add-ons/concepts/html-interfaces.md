# Editor add-on user interfaces

[Editor add-ons](/workspace/add-ons/concepts/types#editor_add-ons) enable user interaction through customized menus, dialogs, and sidebars. The following links provide information building these types of interfaces.

- [Add-on menus](/workspace/add-ons/concepts/menus) are created using Google Apps Script's base [Ui service](/apps-script/reference/base/ui). Menu items provide starting points for using your add-on, but you must design them to take into account the add-on [authorization lifecycle](/workspace/add-ons/concepts/editor-auth-lifecycle#the_complete_lifecycle).
- [Sidebars and dialogs](/workspace/add-ons/concepts/dialogs) are created using Apps Script's [HTML service](/apps-script/reference/html). This service lets you define the interface structure and appearance using HTML and CSS. See [Create and serve HTML](/apps-script/guides/html) for more details.
  - Set up [client-server communication](/apps-script/guides/html/communication) calls so user actions in the interface result in actions taken on the Google servers where the editor file resides or vice-versa.
  - Apps Script also provides a [template syntax](/apps-script/guides/html/templates) to make building dynamic interfaces easier.

- When building HTML interfaces for Editor add-ons, use the [Editor add-on CSS package](/workspace/add-ons/guides/css) to help your add-on look and feel like the Google Workspace editors they extend.
