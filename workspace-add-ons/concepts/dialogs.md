# Dialogs and sidebars for Editor add-on

For most [Editor add-ons](/workspace/add-ons/concepts/types#editor_add-ons), dialog windows and sidebar panels are the primary add-on user interfaces. Both are fully customizable using standard HTML and CSS, and you can use Google Apps Script's [client-server communication model](/apps-script/guides/html/communication) to run Apps Script functions when the user interacts with the sidebar or dialog. Your add-on can define multiple sidebars and dialogs, but the add-on can display only one at a time.

When you want to prevent the user from interacting with the editor until they make some choice in the add-on interface, use a dialog; otherwise use a sidebar.

## Dialogs

*Dialogs* are window panels that overlay the primary editor content. Apps Script dialogs are modal; while they are opened the user can't interact with the other elements of the editor interface. You can customize the content and size of dialogs.

You build add-on dialogs the same way as Apps Script [custom dialogs](/apps-script/guides/dialogs#custom_dialogs). The general procedure is:

1. Create a script project file that defines your dialog's HTML structure, CSS, and client-side JavaScript behavior. Refer to the [Editor add-on style guidelines](/workspace/add-ons/guides/editor-style#dialogs).
2. In your server-side code where you want the dialog to open, call [`HtmlService.createHtmlOutputFromFile`](/apps-script/reference/html/html-service#createhtmloutputfromfilefilename) to create an [`HtmlOutput`](/apps-script/reference/html/html-output) object representing the dialog. Alternatively, if you are using [templated HTML](/apps-script/guides/html/templates) you can call [`HtmlService.createTemplateFromFile`](/apps-script/reference/html/html-service#createtemplatefromfilefilename) to generate a template and then [`HtmlTemplate.evaluate`](/apps-script/reference/html/html-template#evaluate()) to convert it to an [`HtmlOutput`](/apps-script/reference/html/html-output) object.
3. Call [`Ui.showModalDialog`](/apps-script/reference/base/ui#showModalDialog(Object,String)) to display the dialog using that [`HtmlOutput`](/apps-script/reference/html/html-output).

Dialogs don't suspend the server-side script while they are open. The client-side JavaScript can make asynchronous calls to the server-side using [`google.script.run`](/apps-script/guides/html/reference/run) and associated handler functions. For more details, see [Client-to-server communication](/apps-script/guides/html/communication).

### File-open dialogs

*File-open dialogs* are prebuilt dialogs that let your users select files from their Google Drive. You can add a file-open dialog to your add-on without needing to design it, but it requires some additional configuration. You also require access to the add-on's [Cloud Platform project](/apps-script/guides/cloud-platform-projects) in order to enable the Google Picker API.

For more information, see [File-open dialogs](/apps-script/guides/dialogs#file-open_dialogs).

## Sidebars

*Sidebars* are panels that appear in the right of the editor interface, and are the most common type of add-on interface. Unlike dialogs, you can continue to interact with the other elements of the editor interface while a sidebar is open. Sidebars have a fixed width, but you can customize their content.

You build add-on sidebars the same way as Apps Script [custom sidebars](/apps-script/guides/dialogs#custom_sidebars). The general procedure is:

1. Create a script project file that defines your sidebar's HTML structure, CSS, and client-side JavaScript behavior. When defining the sidebar, refer to the [Editor add-on style guidelines](/workspace/add-ons/guides/editor-style#sidebars).
2. In your server-side code where you want the sidebar to open, call [`HtmlService.createHtmlOutputFromFile`](/apps-script/reference/html/html-service#createhtmloutputfromfilefilename) to create an [`HtmlOutput`](/apps-script/reference/html/html-output) object representing the sidebar. Alternatively, if you are using [templated HTML](/apps-script/guides/html/templates) you can call [`HtmlService.createTemplateFromFile`](/apps-script/reference/html/html-service#createtemplatefromfilefilename) to generate a template and then [`HtmlTemplate.evaluate`](/apps-script/reference/html/html-template#evaluate()) to convert it to an [`HtmlOutput`](/apps-script/reference/html/html-output) object. Add-on sidebars have a fixed width of 300 pixels that you can't alter by calling [`HtmlOutput.setWidth`](/apps-script/reference/html/html-output#setwidthwidth).
3. Call [`Ui.showSidebar`](/apps-script/reference/base/ui#showSidebar(Object)) to display the sidebar using that [`HtmlOutput`](/apps-script/reference/html/html-output).

Sidebars don't suspend the server-side script while they are open. The client-side JavaScript can make asynchronous calls to the server-side using [`google.script.run`](/apps-script/guides/html/reference/run) and associated handler functions. For more details, see [Client-to-server communication](/apps-script/guides/html/communication).
