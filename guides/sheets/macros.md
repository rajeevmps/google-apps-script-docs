# Google Sheets Macros

## Page Summary

- Google Sheets macros automate UI interactions and can be linked to keyboard shortcuts or accessed via the Extensions menu.
- Recording a macro automatically creates an Apps Script function in a bound project's `macros.gs` file and updates the project manifest.
- Macros can be created or edited directly within the Apps Script editor, or existing Apps Script functions can be imported as macros.
- The manifest file structure defines the name, function, and optional keyboard shortcut for each macro.
- Macros are limited to bound scripts in Google Sheets and cannot be used in standalone scripts, web apps, add-ons, libraries, or other Google Workspace applications.

Google Sheets lets you record
[macros](https://support.google.com/docs/answer/7665004) that duplicate a
specific series of UI interactions that you define. Once you've recorded a
macro, you can link it to a keyboard shortcut in the form
`Ctrl+Alt+Shift+Number`. Use that shortcut to quickly execute the
exact macro steps again, typically in a different place or on different data.
You can also activate the macro from the Sheets **Extensions**
> **Macros** menu.

When you record a macro, Sheets automatically creates an
Apps Script function (the *macro function*) that replicates the
macro steps. The macro function is added to an Apps Script
project [bound](https://developers.google.com/apps-script/guides/bound) to the sheet, in a file titled
`macros.gs`. In the event that there is already a project file bound to the
sheet with that name, the macro function is appended to it.
Sheets also automatically updates the script project
[manifest](https://developers.google.com/apps-script/concepts/manifests), recording the name and keyboard
shortcut assigned to the macro.

Since every recorded macro is defined entirely within
Apps Script, you can edit them directly within the
Apps Script editor. You can even write macros from scratch in
Apps Script, or take functions you've already written and turn
them into macros.

## Create macros in Apps Script

You can take functions written in Apps Script and use them as
macro functions. A straightforward way to do this is by importing an existing
function from the Sheets editor.

Alternatively, you can create macros within the Apps Script
editor by following these steps:

1. In the Sheets UI, select **Extensions** >
**Apps Script** to open the
script bound to the sheet in the Apps Script editor.
2. Write the macro function. Macro functions should take no arguments and return
no values.
3. Edit your [script manifest](https://developers.google.com/apps-script/concepts/manifests#editing_a_manifest)
to create the macro and link it to the macro function. Assign it a unique
keyboard shortcut and name.
4. Save the script project. The macro is then available for use in the sheet.
5. Test the macro function in the sheet to verify that functions as intended.

## Edit macros

To edit macros attached to a sheet, do the following:

1. In the Sheets UI, select **Extensions** >
**Macros** > **Manage macros**.
2. Find the macro you want to edit and select
**more_vert > Edit macro**. This opens
the Apps Script editor to the project file containing the
macro function.
3. Edit the macro function to change the macro behavior.
4. Save the script project. The macro is then available for use in the sheet.
5. Test the macro function in the sheet to verify that functions as intended.

## Import functions as macros

If there is already a script [bound](https://developers.google.com/apps-script/guides/bound) to a sheet,
you can *import* a function in the script as a new macro and then assign it
a keyboard shortcut. Do this by
[editing the manifest](https://developers.google.com/apps-script/concepts/manifests#editing_a_manifest)
file and adding another element to the
`sheets.macros[]` property.

Alternatively, follow these steps to import a function as a macro from the
Sheets UI:

1. In the Sheets UI, select **Extensions** >
**Macros** > **Import**.
2. Select a function from the list presented and then click **Add function**.
3. Select clear to close the dialog.
4. Select **Extensions** > **Macros**
> **Manage macros**.
5. Locate the function you just imported in the list. Assign a unique keyboard
shortcut to the macro. You can also change the macro name here; the name
defaults to the name of the function.
6. Click **Update** to save the macro configuration.

## Manifest structure for macros

The following manifest file example snippet shows the section of a
[manifest](https://developers.google.com/apps-script/concepts/manifests) that defines Sheets
macros.
The `sheets` section of the manifest defines the name and keyboard shortcut
assigned to the macro and the name of the macro function.

Manifests include other components that relate to Apps Script
properties. The fields under the `sheets` key relate directly to
Sheets functionality. This example is just a portion of a full
manifest file and is not a fully functional manifest.

```json
{
  ...
  "sheets": {
    "macros": [{
      "menuName": "QuickRowSum",
      "functionName": "calculateRowSum",
      "defaultShortcut": "Ctrl+Alt+Shift+1"
    }, {
      "menuName": "Headerfy",
      "functionName": "updateToHeaderStyle",
      "defaultShortcut": "Ctrl+Alt+Shift+2"
    }]
  }
}
```

See the [Sheets macro manifest resource](https://developers.google.com/apps-script/manifest/sheets)
for more details on how Sheets macro manifests are constructed.

## Best practices

When creating or managing macros in Apps Script, follow these guidelines:

1. Macros are more performant when they are lightweight. Where possible, limit
the number of actions a macro takes.
2. Macros are best suited for rote operations that need to be repeated
frequently with little or no configuration. For other operations, consider
using a [custom menu item](https://developers.google.com/apps-script/guides/menus) instead.
3. Always remember that macro keyboard shortcuts must be unique, and a given
sheet can only have ten macros with shortcuts at any one time. Any additional
macros can only be executed from the **Extensions** >
**Macros** menu.
4. Macros that make changes to a single cell can be applied to a range of
cells by first selecting the full range and then activating the macro.
This means it is often unnecessary to create macros that duplicate the
same operation across a predefined range of cells.

## Things you can't do

There are a few restrictions on what you can do with macros:

#### Use macros outside bound scripts

Macros are defined in scripts bound to specific Sheets. Macro
definitions are ignored if defined in a
[standalone script](https://developers.google.com/apps-script/guides/standalone) or
[web app](https://developers.google.com/apps-script/guides/web).

#### Define macros in Sheets Google Workspace add-ons

You cannot distribute macro definitions using a
[Sheets Google Workspace add-on](https://developers.google.com/workspace/add-ons/overview).
Any macro definitions in a Sheets
add-on project are ignored by users of that
add-on.

#### Distribute macros in script libraries

You cannot distribute macro definitions using Apps Script
[libraries](https://developers.google.com/apps-script/guides/libraries).

#### Use macros outside of Sheets

Macros are only a feature in Sheets, and don't exist for
Google Docs, Forms, or Google Slides.
