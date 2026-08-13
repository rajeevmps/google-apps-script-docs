# Custom Menus in Google Workspace

Scripts can extend certain Google products by adding user-interface elements
that, when clicked, execute an Google Apps Script function. The most common
example is running a script from a custom menu item in Google Docs,
Google Sheets, Google Slides, or Google Forms, but script functions can
also be triggered by clicking on images and drawings in Sheets.

## Custom menus in Docs, Sheets, Slides, or Forms

![](https://developers.google.com/static/apps-script/images/menus.png)

Apps Script can add new menus in Docs,
Sheets, Slides, or Forms, with each
menu item tied to a function in a script. (In Forms, custom
menus are visible only to an editor who opens the form to modify it, not to a
user who opens the form to respond.)

Only bound scripts can create menus. To display the menu when the user opens a
file, write the menu code within an
[`onOpen`](https://developers.google.com/apps-script/understanding_triggers) function.

The following example shows how to add a [menu](https://developers.google.com/apps-script/reference/base/menu)
with one item, followed by a
[visual separator](https://developers.google.com/apps-script/reference/base/menu#addSeparator()), then a
[sub-menu](https://developers.google.com/apps-script/reference/base/menu#addSubMenu(Menu)) that contains
another item. When the user selects either
menu item, a corresponding function opens an
[alert](https://developers.google.com/apps-script/reference/base/ui#alert(String)) dialog. For more
information on the types of dialogs you can open, see the
[guide to dialogs and sidebars](https://developers.google.com/apps-script/guides/dialogs).

    function onOpen() {
      const ui = SpreadsheetApp.getUi();
      // Or DocumentApp, SlidesApp or FormApp.
      ui.createMenu('Custom Menu')
          .addItem('First item', 'menuItem1')
          .addSeparator()
          .addSubMenu(ui.createMenu('Sub-menu')
              .addItem('Second item', 'menuItem2'))
          .addToUi();
    }

    function menuItem1() {
      SpreadsheetApp.getUi() // Or DocumentApp, SlidesApp or FormApp.
          .alert('You clicked the first menu item!');
    }

    function menuItem2() {
      SpreadsheetApp.getUi() // Or DocumentApp, SlidesApp or FormApp.
          .alert('You clicked the second menu item!');
    }

A document, spreadsheet, presentation, or form can only contain one menu with
a given name. If the same script or another script adds a menu with the same
name, the new menu replaces the old. Menus cannot be removed while the file
is open, although you can write your `onOpen` function to skip the menu in
the future if a certain [property](https://developers.google.com/apps-script/guides/properties) is set.

[Editor add-ons](https://developers.google.com/workspace/add-ons/concepts/types#editor_add-ons)
can have menu items as well, but use
[special rules](https://developers.google.com/workspace/add-ons/concepts/menus) for how
they are defined.

## Clickable images and drawings in Sheets

![](https://developers.google.com/static/apps-script/images/drawing.png)

You can also assign an Apps Script function to an image or
drawing in Sheets, provided the script is bound to the
spreadsheet. The following example shows how to set this up.

1. In Sheets, select the menu item **Extensions** \> **Apps Script** to create a script that is bound to the spreadsheet.
2. Delete any code in the script editor and paste in the code below.

    function showMessageBox() {
      SpreadsheetApp.getUi().alert('You clicked it!');
    }

1. Return to Sheets and insert an image or drawing by selecting **Insert \> Image** or **Insert \> Drawing**.
2. After inserting the image or drawing, click it. A small drop-down menu selector appears in the top right-hand corner. Click it and choose **Assign script**.
3. In the dialog that appears, type the name of the Apps Script function that you want to run, without parentheses --- in this case, `showMessageBox`. Click **OK**.
4. Click the image or drawing again. The function now executes.

The script execution is only triggered by clicking the image or drawing in a web browser.
The script doesn't execute if the image or drawing is clicked on mobile.

# Dialogs and Sidebars in Google Workspace Documents

Google Apps Script projects [bound](https://developers.google.com/apps-script/scripts_containers) to
Google Docs, Google Sheets, or Google Forms can display
user-interface elements, such as prebuilt alerts, prompts, toasts, dialogs, and
sidebars. These elements typically contain custom
[HTML service](https://developers.google.com/apps-script/guides/html) content and are often opened from
[menu items](https://developers.google.com/apps-script/guides/menus). In Forms, user-interface
elements are visible only to an editor who opens the form to modify it, not to a
respondent.

## Alert dialogs

![](https://developers.google.com/static/apps-script/images/alert.png)

An alert is a prebuilt dialog that opens inside a Docs,
Sheets, Slides, or Forms editor. It
displays a message and an **OK** button; a title and alternative buttons are
optional. It is similar to calling
[`window.alert`](https://developer.mozilla.org/en-US/docs/Web/API/window.alert)
in client-side JavaScript within a web browser.

Alerts suspend the server-side script while the dialog is open. The script
resumes after the user closes the dialog, but [JDBC](https://developers.google.com/apps-script/guides/jdbc)
connections don't persist across the suspension.

As shown in the following example, Docs, Forms,
Slides, and Sheets all use the method
[`Ui.alert`](https://developers.google.com/apps-script/reference/base/ui#alert(String)), which is available
in three variants. To override the default **OK** button, pass a value from the
[`Ui.ButtonSet`](https://developers.google.com/apps-script/reference/base/button-set) enum as the `buttons`
argument. To evaluate which button the user clicked, compare the return value
for `alert` to the [`Ui.Button`](https://developers.google.com/apps-script/reference/base/button) enum.

    function onOpen() {
      SpreadsheetApp.getUi() // Or DocumentApp or SlidesApp or FormApp.
        .createMenu("Custom Menu")
        .addItem("Show alert", "showAlert")
        .addToUi();
    }

    function showAlert() {
      const ui = SpreadsheetApp.getUi(); // Same variations.

      const result = ui.alert(
        "Please confirm",
        "Are you sure you want to continue?",
        ui.ButtonSet.YES_NO,
      );

      // Process the user's response.
      if (result === ui.Button.YES) {
        // User clicked "Yes".
        ui.alert("Confirmation received.");
      } else {
        // User clicked "No" or X in the title bar.
        ui.alert("Permission denied.");
      }
    }

## Prompt dialogs

![](https://developers.google.com/static/apps-script/images/prompt.png)

A prompt is a prebuilt dialog that opens inside a Docs,
Sheets, Slides, or Forms editor. It
displays a message, a text-input field, and an **OK** button; a title and
alternative buttons are optional. It is similar to calling
[`window.prompt`](https://developer.mozilla.org/en-US/docs/Web/API/window.prompt)
in client-side JavaScript within a web browser.

Prompts suspend the server-side script while the dialog is open. The script
resumes after the user closes the dialog, but [JDBC](https://developers.google.com/apps-script/guides/jdbc)
connections don't persist across the suspension.

As shown in the following example, Docs, Forms,
Slides, and Sheets all use the method
[`Ui.prompt`](https://developers.google.com/apps-script/reference/base/ui#prompt(String)), which is
available in three variants. To override the default **OK** button, pass a value
from the [`Ui.ButtonSet`](https://developers.google.com/apps-script/reference/base/button-set) enum as the
`buttons` argument. To evaluate the user's response, capture the return value
for `prompt`, then call
[`PromptResponse.getResponseText`](https://developers.google.com/apps-script/reference/base/prompt-response#getResponseText())
to retrieve the user's input, and compare the return value for
[`PromptResponse.getSelectedButton`](https://developers.google.com/apps-script/reference/base/prompt-response#getSelectedButton())
to the [`Ui.Button`](https://developers.google.com/apps-script/reference/base/button) enum.

    function onOpen() {
      SpreadsheetApp.getUi() // Or DocumentApp or SlidesApp or FormApp.
        .createMenu("Custom Menu")
        .addItem("Show prompt", "showPrompt")
        .addToUi();
    }

    function showPrompt() {
      const ui = SpreadsheetApp.getUi(); // Same variations.

      const result = ui.prompt(
        "Let's get to know each other!",
        "Please enter your name:",
        ui.ButtonSet.OK_CANCEL,
      );

      // Process the user's response.
      const button = result.getSelectedButton();
      const text = result.getResponseText();
      if (button === ui.Button.OK) {
        // User clicked "OK".
        ui.alert("Your name is " + text + ".");
      } else if (button === ui.Button.CANCEL) {
        // User clicked "Cancel".
        ui.alert("I didn't get your name.");
      } else if (button === ui.Button.CLOSE) {
        // User clicked X in the title bar.
        ui.alert("You closed the dialog.");
      }
    }

## Spreadsheet toasts

A "toast" is a small dialog window in the lower right corner of a
Sheets editor that displays a message but does not suspend the
script. It is a good way to show status messages or updates that don't require
user interaction.

As shown in the following example, Sheets uses the method
[`Spreadsheet.toast`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#toast(String)).
Toasts are only available in Sheets.

    function showToast() {
      SpreadsheetApp.getActiveSpreadsheet().toast("Task completed successfully.");
    }

## Custom dialogs

![](https://developers.google.com/static/apps-script/images/dialog.png)

A custom dialog can display an [HTML service](https://developers.google.com/apps-script/guides/html) user
interface inside a Docs, Sheets,
Slides, or Forms editor.

Custom dialogs do *not* suspend the server-side script while the dialog is open.
Because they are asynchronous, the server-side function that opens the dialog
finishes immediately. To pass data from the custom dialog back to the server,
use the [`google.script`](https://developers.google.com/apps-script/guides/html/communication) API in your
client-side code.

The dialog can close itself by calling
[`google.script.host.close`](https://developers.google.com/apps-script/guides/html/communication#closing_dialogs_and_sidebars_in_google_apps)
in the client side of an HTML-service interface. The dialog cannot be closed by
other interfaces, only by the user or itself.

As shown in the following example, Docs, Forms,
Slides, and Sheets all use the method
[`Ui.showModalDialog`](https://developers.google.com/apps-script/reference/base/ui#showModalDialog(Object,String))
to open the dialog.

### Code.gs

```
function onOpen() {
  SpreadsheetApp.getUi() // Or DocumentApp or SlidesApp or FormApp.
      .createMenu('Custom Menu')
      .addItem('Show dialog', 'showDialog')
      .addToUi();
}

function showDialog() {
  const html = HtmlService.createHtmlOutputFromFile('Page')
      .setWidth(400)
      .setHeight(300);
  SpreadsheetApp.getUi() // Or DocumentApp or SlidesApp or FormApp.
      .showModalDialog(html, 'My custom dialog');
}
```

### Page.html

```html
Hello, world! <input type="button" value="Close" onclick="google.script.host.close()" />
```

## Custom sidebars

![](https://developers.google.com/static/apps-script/images/sidebar.png)

A sidebar can display an [HTML service](https://developers.google.com/apps-script/guides/html) user
interface inside a Docs, Forms,
Slides, and Sheets editor.

Sidebars do *not* suspend the server-side script while the dialog is open. The
client-side component can make asynchronous calls to the server-side script
using the [`google.script`](https://developers.google.com/apps-script/guides/html/communication) API for
HTML-service interfaces.

The sidebar can close itself by calling
[`google.script.host.close`](https://developers.google.com/apps-script/guides/html/communication#closing_dialogs_and_sidebars_in_google_apps)
in the client side of an HTML-service interface. The sidebar cannot be closed by
other interfaces, only by the user or itself.

As shown in the following example, Docs, Forms,
Slides, and Sheets all use the method
[`Ui.showSidebar`](https://developers.google.com/apps-script/reference/base/ui#showSidebar(Object)) to open
the sidebar.

### Code.gs

```
function onOpen() {
  SpreadsheetApp.getUi() // Or DocumentApp or SlidesApp or FormApp.
      .createMenu('Custom Menu')
      .addItem('Show sidebar', 'showSidebar')
      .addToUi();
}

function showSidebar() {
  const html = HtmlService.createHtmlOutputFromFile('Page')
      .setTitle('My custom sidebar');
  SpreadsheetApp.getUi() // Or DocumentApp or SlidesApp or FormApp.
      .showSidebar(html);
}
```

### Page.html

```html
Hello, world! <input type="button" value="Close" onclick="google.script.host.close()" />
```

## File-open dialogs

[Google Picker](https://developers.google.com/picker) is a JavaScript API that lets users select or
upload Google Drive files. Use the Google Picker library in
[HTML service](https://developers.google.com/apps-script/guides/html) to create a custom dialog that lets
users select existing files or upload new ones, then pass the selection back to
your script.

### Requirements

Using [Google Picker](https://developers.google.com/picker) with Google Apps Script has several
requirements:

- [Set up your environment](https://developers.google.com/drive/picker/guides/overview#setup)
  for Google Picker.

- Your script project must use a [standard
  Google Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#standard_cloud_platform_projects).

  Pass the same Cloud project number to
  [`PickerBuilder.setAppId`](https://developers.google.com/drive/picker/reference/picker.pickerbuilder.setappid)
  if using the `drive.file` scope.
- The Apps Script [project
  manifest](https://developers.google.com/apps-script/concepts/manifests) must specify the authorization
  scopes required by the Google Picker API so that
  [`ScriptApp.getOAuthToken`](https://developers.google.com/apps-script/reference/script/script-app#getOAuthToken())
  returns the correct token for
  [`PickerBuilder.setOauthtoken`](https://developers.google.com/drive/picker/reference/picker.pickerbuilder.setoauthtoken).

- Restrict the API key set in
  [`PickerBuilder.setDeveloperKey`](https://developers.google.com/drive/picker/reference/picker.pickerbuilder.setdeveloperkey)
  to Apps Script. Under **Application restrictions**, follow
  these steps:

  1. Select **HTTP referrers (web sites)**.
  2. Under **Website restrictions** , click **Add an item**.
  3. Click **Referrer** and enter `*.google.com`.
  4. Add another item and enter `*.googleusercontent.com` as the referrer.
  5. Click **Done**.
- Call
  [`PickerBuilder.setOrigin`](https://developers.google.com/drive/picker/reference/picker.pickerbuilder.setorigin).

### Example

The following example shows Google Picker in Apps Script.

### code.gs

picker/code.gs [View on GitHub](https://github.com/googleworkspace/apps-script-samples/blob/main/picker/code.gs)

```javascript
/**
 * Creates a custom menu in Google Sheets when the spreadsheet opens.
 */
function onOpen() {
  SpreadsheetApp.getUi()
    .createMenu("Picker")
    .addItem("Start", "showPicker")
    .addToUi();
}

/**
 * Displays an HTML-service dialog in Google Sheets that contains client-side
 * JavaScript code for the Google Picker API.
 */
function showPicker() {
  const html = HtmlService.createHtmlOutputFromFile("dialog.html")
    .setWidth(800)
    .setHeight(600)
    .setSandboxMode(HtmlService.SandboxMode.IFRAME);
  SpreadsheetApp.getUi().showModalDialog(html, "Select a file");
}
// Ensure the Drive API is enabled.
if (!Drive) {
  throw new Error("Please enable the Drive advanced service.");
}

/**
 * Checks that the file can be accessed.
 * @param {string} fileId The ID of the file.
 * @return {Object} The file resource.
 */
function getFile(fileId) {
  return Drive.Files.get(fileId, { fields: "*" });
}

/**
 * Gets the user's OAuth 2.0 access token so that it can be passed to Picker.
 * This technique keeps Picker from needing to show its own authorization
 * dialog, but is only possible if the OAuth scope that Picker needs is
 * available in Apps Script. In this case, the function includes an unused call
 * to a DriveApp method to ensure that Apps Script requests access to all files
 * in the user's Drive.
 *
 * @return {string} The user's OAuth 2.0 access token.
 */
function getOAuthToken() {
  return ScriptApp.getOAuthToken();
}
```

### dialog.html

picker/dialog.html [View on GitHub](https://github.com/googleworkspace/apps-script-samples/blob/main/picker/dialog.html)

```html
<!DOCTYPE html>
<html>
  <head>
    <link
      rel="stylesheet"
      href="https://ssl.gstatic.com/docs/script/css/add-ons.css"
    />
    <style>
      #result {
        display: flex;
        flex-direction: column;
        gap: 0.25em;
      }

      pre {
        font-size: x-small;
        max-height: 25vh;
        overflow-y: scroll;
        background: #eeeeee;
        padding: 1em;
        border: 1px solid #cccccc;
      }
    </style>
    <script>
      // TODO: Replace the value for DEVELOPER_KEY with the API key obtained
      // from the Google Developers Console.
      const DEVELOPER_KEY = "AIza...";
      // TODO: Replace the value for CLOUD_PROJECT_NUMBER with the project
      // number obtained from the Google Developers Console.
      const CLOUD_PROJECT_NUMBER = "1234567890";

      let pickerApiLoaded = false;
      let oauthToken;

      /**
       * Loads the Google Picker API.
       */
      function onApiLoad() {
        gapi.load("picker", {
          callback: function () {
            pickerApiLoaded = true;
          },
        });
      }

      /**
       * Gets the user's OAuth 2.0 access token from the server-side script so that
       * it can be passed to Picker. This technique keeps Picker from needing to
       * show its own authorization dialog, but is only possible if the OAuth scope
       * that Picker needs is available in Apps Script. Otherwise, your Picker code
       * will need to declare its own OAuth scopes.
       */
      function getOAuthToken() {
        google.script.run
          .withSuccessHandler((token) => {
            oauthToken = token;
            createPicker(token);
          })
          .withFailureHandler(showError)
          .getOAuthToken();
      }

      /**
       * Creates a Picker that can access the user's spreadsheets. This function
       * uses advanced options to hide the Picker's left navigation panel and
       * default title bar.
       *
       * @param {string} token An OAuth 2.0 access token that lets Picker access the
       *     file type specified in the addView call.
       */
      function createPicker(token) {
        document.getElementById("result").innerHTML = "";

        if (pickerApiLoaded && token) {
          const picker = new google.picker.PickerBuilder()
            // Instruct Picker to display only spreadsheets in Drive. For other
            // views, see https://developers.google.com/picker/reference/picker.viewid
            .addView(
              new google.picker.DocsView(
                google.picker.ViewId.SPREADSHEETS
              ).setOwnedByMe(true)
            )
            // Hide the navigation panel so that Picker fills more of the dialog.
            .enableFeature(google.picker.Feature.NAV_HIDDEN)
            // Hide the title bar since an Apps Script dialog already has a title.
            .hideTitleBar()
            .setOAuthToken(token)
            .setDeveloperKey(DEVELOPER_KEY)
            .setAppId(CLOUD_PROJECT_NUMBER)
            .setCallback(pickerCallback)
            .setOrigin(google.script.host.origin)
            .build();
          picker.setVisible(true);
        } else {
          showError("Unable to load the file picker.");
        }
      }

      /**
       * @typedef {Object} PickerResponse
       * @property {string} action
       * @property {PickerDocument[]} docs
       */

      /**
       * @typedef {Object} PickerDocument
       * @property {string} id
       * @property {string} name
       * @property {string} mimeType
       * @property {string} url
       * @property {string} lastEditedUtc
       */

      /**
       * A callback function that extracts the chosen document's metadata from the
       * response object. For details on the response object, see
       * https://developers.google.com/picker/reference/picker.responseobject
       *
       * @param {PickerResponse} data The response object.
       */
      function pickerCallback(data) {
        const action = data[google.picker.Response.ACTION];
        if (action == google.picker.Action.PICKED) {
          handlePicked(data);
        } else if (action == google.picker.Action.CANCEL) {
          document.getElementById("result").innerHTML = "Picker canceled.";
        }
      }

      /**
       * Handles `"PICKED"` responsed from the Google Picker.
       *
       * @param {PickerResponse} data The response object.
       */
      function handlePicked(data) {
        const doc = data[google.picker.Response.DOCUMENTS][0];
        const id = doc[google.picker.Document.ID];

        google.script.run
          .withSuccessHandler((driveFilesGetResponse) => {
            // Render the response from Picker and the Drive.Files.Get API.
            const resultElement = document.getElementById("result");
            resultElement.innerHTML = "";

            for (const response of [
              {
                title: "Picker response",
                content: JSON.stringify(data, null, 2),
              },
              {
                title: "Drive.Files.Get response",
                content: JSON.stringify(driveFilesGetResponse, null, 2),
              },
            ]) {
              const titleElement = document.createElement("h3");
              titleElement.appendChild(document.createTextNode(response.title));
              resultElement.appendChild(titleElement);

              const contentElement = document.createElement("pre");
              contentElement.appendChild(
                document.createTextNode(response.content)
              );
              resultElement.appendChild(contentElement);
            }
          })
          .withFailureHandler(showError)
          .getFile(data[google.picker.Response.DOCUMENTS][0].id);
      }

      /**
       * Displays an error message within the #result element.
       *
       * @param {string} message The error message to display.
       */
      function showError(message) {
        document.getElementById("result").innerHTML = "Error: " + message;
      }
    </script>
  </head>

  <body>
    <div>
      <button onclick="getOAuthToken()">Select a file</button>
      <div id="result"></div>
    </div>
    <script src="https://apis.google.com/js/api.js?onload=onApiLoad"></script>
  </body>
</html>
```

### appsscript.json

picker/appsscript.json [View on GitHub](https://github.com/googleworkspace/apps-script-samples/blob/main/picker/appsscript.json)

```json
{
  "timeZone": "America/Los_Angeles",
  "exceptionLogging": "STACKDRIVER",
  "runtimeVersion": "V8",
  "oauthScopes": [
    "https://www.googleapis.com/auth/script.container.ui",
    "https://www.googleapis.com/auth/drive.file"
  ],
  "dependencies": {
    "enabledAdvancedServices": [
      {
        "userSymbol": "Drive",
        "version": "v3",
        "serviceId": "drive"
      }
    ]
  }
}
```
