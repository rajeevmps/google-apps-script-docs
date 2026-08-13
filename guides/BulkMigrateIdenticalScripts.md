# Bulk migrate identical scripts from Rhino to V8

This page describes how to migrate identical scripts to V8 using
Google Apps Script and the Apps Script API.

The Rhino runtime was turned down on or after January 31, 2026. Migrate
any scripts that use the Rhino runtime before that date. If you have multiple,
identical scripts running on Rhino, migrate them to V8 all together using the
Apps Script API.

## Set up your environment

1. From the Apps Script dashboard settings, turn on the Apps Script API.
   1. Go to the [Apps Script dashboard
      settings](https://script.google.com/home/usersettings).
   2. If the API is turned off, click **Apps Script API** , then turn on the **Apps Script API** toggle.
2. [Create a standard Google Cloud project](https://developers.google.com/workspace/guides/create-project#project) or reuse an existing project.
3. In your Cloud project, [configure the OAuth consent
   screen](https://developers.google.com/workspace/guides/configure-oauth-consent).
4. In your Cloud project, [turn on the
   Apps Script API](https://developers.google.com/workspace/guides/enable-apis).

   [Turn on the Apps Script API](https://console.cloud.google.com/flows/enableapi?apiid=script.googleapis.com)
5. Create an Apps Script project and assign it to your
   Cloud project.

   1. Create a standalone Apps Script project from the Apps Script dashboard or by going to [script.new](https://script.google.com/home/projects/create).
   2. Click **Project Settings** ![The icon for project settings](https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/settings/default/24px.svg).
   3. In the **Google Cloud Project** section, click **Change project**.
   4. Enter the project number of your Cloud project.
   5. Click **Set project**.

## Migrate scripts

The following code sample shows how to use the Apps Script API to
migrate identical scripts from Rhino to V8 by replacing the files in each
Apps Script project with a set of V8-compatible files.

When you use the
[`projects.UpdateContent`](https://developers.google.com/apps-script/api/reference/rest/v1/projects/updateContent)
method of the Apps Script API, include all the files in the script
project, even ones you don't want to change. If you don't include a file, the
file is deleted and can't be restored.

Ensure you have at least editor access to the script projects you plan to
migrate.

### Code.gs

    function updateRhinoScripts() {
      // An array of script IDs of script projects to migrate.
      // TODO(developer): Replace with your script IDs.
      const scriptIds = ['abcdef12345678', 'abcdef12345678'];
      // An array of file objects to replace the existing files in each script project.
      // Remember to include all files for the script, excluded files are deleted.
      // TODO(developer): Replace with your script files.
      const filesToUpdate = {
        "files": [
          {
            "name": "Code",
            "type": "SERVER_JS",
            "source": "// New updates\nfunction myFunction() {\n  console.log('Hello, world!');\n}"
          },
          {
            "name": "appsscript",
            "type": "JSON",
            "source": JSON.stringify({
              "timeZone": "America/New_York",
              "dependencies": {},
              "exceptionLogging": "STACKDRIVER",
              "runtimeVersion": "V8"
            })
          }
        ]
      };
      updateMultipleAppsScripts(scriptIds, filesToUpdate);
    }

    function updateMultipleAppsScripts(scriptIds, filesToUpdate) {
      // 'scriptIds' should be an array of script IDs
      // 'filesToUpdate' should be an array of objects, each with:
      // name: The filename (For example, "Code", "Utilities")
      // source: The source code for that file.
      scriptIds.forEach(function (scriptId) {
        // Makes the API request.
        const response = UrlFetchApp.fetch(
          `https://script.googleapis.com/v1/projects/${scriptId}/content`,
          {
            method: "PUT",
            headers: {
              Authorization: `Bearer ${ScriptApp.getOAuthToken()}`
            },
            contentType: "application/json",
            payload: JSON.stringify(filesToUpdate),
            muteHttpExceptions: true
          }
        );
        if (response.getResponseCode() !== 200) {
          console.log(`Error updating script ${scriptId}: ${response.getContentText()}`);
        } else {
          console.log(`Script ${scriptId} updated successfully!`);
        }
      });
    }

### appsscript.json

To use the Apps Script API in your Apps Script
project, add the following OAuth scopes to your manifest file:

- `"https://www.googleapis.com/auth/script.projects"`
- `"https://www.googleapis.com/auth/script.external_request"`

To expose the manifest file in the editor, click **Project Settings**
![The icon for project settings](https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/settings/default/24px.svg)
and check the **Show "appsscript.json" manifest file in editor** box. The
following is a sample manifest file with the appropriate OAuth scopes:

    {
      "timeZone": "America/Denver",
      "dependencies": {
      },
      "oauthScopes": [
      "https://www.googleapis.com/auth/script.projects",
      "https://www.googleapis.com/auth/script.external_request"
    ],
      "exceptionLogging": "STACKDRIVER",
      "runtimeVersion": "V8"
    }

## Related topics

- [V8 runtime overview](https://developers.google.com/apps-script/guides/v8-runtime)
- [Migrate scripts to the V8 runtime](https://developers.google.com/apps-script/guides/v8-runtime/migration)