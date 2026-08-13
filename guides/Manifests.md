# Manifests

A Google Apps Script project *manifest* is a special JSON file that specifies
basic project information that Apps Script needs to run the
script successfully.

Apps Script automatically creates and updates the project
manifest as you create your script project and make changes in the
Apps Script editor. In most cases, you don't need to view or
edit the manifest directly.

The manifest file structure and its JSON fields are described in the
[Manifest structure](https://developers.google.com/apps-script/manifest) reference guide.

## Editing a manifest

The Apps Script editor hides manifest files by default in order to protect
your Apps Script project settings. Follow these steps to make a hidden project
manifest visible in the Apps Script editor:

1. Open the script project in the Apps Script editor.
2. Click **Project Settings** .
3. Select the **Show "appsscript.json" manifest file in editor** checkbox.

The manifest file appears as a project file named `appsscript.json`. You
can edit this file directly in the editor and save any changes you make. To hide
the manifest file after you make your changes, repeat the previous steps and
clear the **Show "appsscript.json" manifest file in editor** checkbox.

> [!NOTE]
> **Note:** *Hide the manifest when you are done editing.* Your manifest may already contain a number of key:value pairs; these represent the current configuration of your Apps Script project. Exercise care when editing the manifest, as you may inadvertently alter how your script project operates.

> [!WARNING]
> **Warning:** Make sure you define your manifest file correctly. A poorly defined manifest can prevent you from saving a versioned deployment. A script project that you want to publish can't pass publication review if it lacks required fields or uses OAuth scopes that are too broad.