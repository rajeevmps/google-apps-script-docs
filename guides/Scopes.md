# Authorization Scopes

Users must authorize script projects that access their data or act on their
behalf. For a high-level overview of this process, see
[Authorization for Google Services](https://developers.google.com/apps-script/guides/services/authorization).
When a user runs a script that requires authorization for the first
time, the UI presents a prompt to start the authorization flow.

During this flow, the UI tells users which permissions the script requests. For
example, a script might request permission to read email messages or create
calendar events. The script project defines these individual permissions as
*OAuth scopes*.

For most scripts, Apps Script automatically detects required
scopes. You can [view the scopes](https://developers.google.com/apps-script/concepts/scopes#view-scopes) a script uses at any time. You
can also [set scopes explicitly](https://developers.google.com/apps-script/concepts/scopes#set-explicit) in your
[manifest](https://developers.google.com/apps-script/concepts/manifests) using URL strings. Published
applications, such as [add-ons](https://developers.google.com/workspace/add-ons/overview), must use the
narrowest scopes possible.

During the authorization flow, Apps Script presents
human-readable descriptions of the required scopes. For example, if your script
needs read-only access to spreadsheets, the manifest might include the scope
`https://www.googleapis.com/auth/spreadsheets.readonly`. The authorization
prompt asks the user to "View your Google Spreadsheets".

Some scopes include others. For example, authorized access to
`https://www.googleapis.com/auth/spreadsheets` allows read and write access to
spreadsheets.

For some surfaces, such as the Apps Script IDE, users see the
granular OAuth consent screen. This screen lets users select specific
permissions to grant rather than granting all permissions at once. Design your
script to [handle granular OAuth permissions](https://developers.google.com/apps-script/concepts/scopes#handle-granular).

## View scopes

To see the scopes your script project requires:

1. Open the script project.
2. At the left, click **Overview** .
3. View the scopes under **Project OAuth Scopes**.

## Set explicit scopes

Apps Script automatically determines required scopes by scanning
the code for function calls. While this is sufficient for most scripts, you
must exercise more direct control for published add-ons, web
apps, Chat apps, and calls to the Chat API.

Apps Script sometimes automatically assigns permissive scopes.
This can mean your script asks users for more access than it needs. For
published scripts, replace broad scopes with a limited set that covers the
script's needs.

> [!WARNING]
> **Warning:** Always use the least permissive scope set possible. To protect user information, add-ons and other published applications must not ask for more scope permissions than they need.

You can explicitly set the scopes your script project uses by editing its
[manifest](https://developers.google.com/apps-script/concepts/manifests) file. The `oauthScopes` manifest
field is an array of scopes used by the project. To set your project's scopes:

1. Open the script project.
2. At the left, click **Project Settings** .
3. Select the **Show "appsscript.json" manifest file in editor** checkbox.
4. At the left, click **Editor** .
5. At the left, click the `appsscript.json` file.
6. Locate the top-level field labeled `oauthScopes`. If it's not present, you can add it.
7. Replace the contents of the `oauthScopes` array with the scopes you want the project to use. For example:

   ```
         {
           ...
           "oauthScopes": [
             "https://www.googleapis.com/auth/spreadsheets.readonly",
             "https://www.googleapis.com/auth/userinfo.email"
           ],
          ...
         }
   ```
8. At the top, click **Save** .

## Handle granular OAuth permissions

The granular OAuth consent screen first launched to the
Apps Script IDE for users executing a script directly. The
consent screen is progressively released to other surfaces, such as macros, triggers, and
add-ons, over time. For more information, see
[Granular OAuth consent in Google Apps Script IDE executions](https://workspaceupdates.googleblog.com/2025/01/granular-oauth-consent-in-google-apps-script.html).

The granular OAuth consent screen lets users specify which individual OAuth
scopes to authorize. This gives users fine-grained control over what account
data they share with each script. For example, if a script requests email and
calendar scopes, users can choose to grant Calendar permission
but not Gmail.

The following sections describe how to handle granular OAuth permissions.

### Automatically require permission for necessary scopes

If an execution flow requires specific scopes, you can require users to grant
those permissions. Your script can check for permissions and automatically ask
for them if missing.

The following methods from the
[`ScriptApp` class](https://developers.google.com/apps-script/reference/script/script-app) validate
permissions and render the authorization prompt:

- [`requireScopes(authMode, oAuthScopes)`](https://developers.google.com/apps-script/reference/script/script-app#requirescopesauthmode,-oauthscopes): Use this method for flows that rely on specific scopes.
- [`requireAllScopes(authMode)`](https://developers.google.com/apps-script/reference/script/script-app#requireallscopesauthmode): Use this method if an execution flow relies on all project scopes.

#### Example

The following example shows how to call `requireScopes()` and
`requireAllScopes()`. The script uses scopes for Gmail,
Sheets, and Calendar. The `sendEmail()` function
requires only the scopes for Gmail and Sheets
while the `createEventSendEmail()` function requires all scopes used by the
script.

    // This function requires the Gmail and Sheets scopes.
    function sendEmail() {
      // Validates that the user has granted permission for the Gmail and Sheets scopes.
      // If not, the execution ends and prompts the user for authorization.
      ScriptApp.requireScopes(ScriptApp.AuthMode.FULL, [
        'https://mail.google.com/',
        'https://www.googleapis.com/auth/spreadsheets'
      ]);

      // Sends an email.
      GmailApp.sendEmail("dana@example.com", "Subject", "Body");
      Logger.log("Email sent successfully!");

      // Opens a spreadsheet and sheet to track the sent email.
      const ss = SpreadsheetApp.openById("abc1234567");
      const sheet = ss.getSheetByName("Email Tracker")

      // Gets the last row of the sheet.
      const lastRow = sheet.getLastRow();

      // Adds "Sent" to column E of the last row of the spreadsheet.
      sheet.getRange(lastRow, 5).setValue("Sent");
      Logger.log("Sheet updated successfully!");
    }

    // This function requires all scopes used by the script (Gmail,
    // Calendar, and Sheets).
    function createEventSendEmail() {
      // Validates that the user has granted permission for all scopes used by the
      // script. If not, the execution ends and prompts the user for authorization.
      ScriptApp.requireAllScopes(ScriptApp.AuthMode.FULL);

      // Creates an event.
      CalendarApp.getDefaultCalendar().createEvent(
        "Meeting",
        new Date("November 28, 2024 10:00:00"),
        new Date("November 28, 2024 11:00:00")
      );
      Logger.log("Calendar event created successfully!");

      // Sends an email.
      GmailApp.sendEmail("dana@example.com", "Subject 2", "Body 2");
      Logger.log("Email sent successfully!");

      // Opens a spreadsheet and sheet to track the created meeting and sent email.
      const ss = SpreadsheetApp.openById("abc1234567");
      const sheet = ss.getSheetByName("Email and Meeting Tracker")
      // Gets the last row
      const lastRow = sheet.getLastRow();

      // Adds "Sent" to column E of the last row
      sheet.getRange(lastRow, 5).setValue("Sent");
      // Adds "Meeting created" to column F of the last row
      sheet.getRange(lastRow, 6).setValue("Meeting created");
      Logger.log("Sheet updated successfully!");
    }

### Create a custom experience for missing scopes

You can retrieve the permission status of users and design custom experiences.
For example, you might disable features that require missing permissions or
display a dialog explaining the requirement. The following methods retrieve
an object with the user's permission information that includes which scopes
the user has authorized and a URL to request any missing scopes:

- [`getAuthorizationInfo(authMode, oAuthScopes)`](https://developers.google.com/apps-script/reference/script/script-app#getauthorizationinfoauthmode,-oauthscopes): Checks permission status for specific scopes.
- [`getAuthorizationInfo(authMode)`](https://developers.google.com/apps-script/reference/script/script-app#getauthorizationinfoauthmode): Checks permission status for all project scopes.

To get the permission details from the authorization info object, such as the
list of authorized scopes and the URL to request missing permissions, use the
methods from the
[`AuthorizationInfo` class](https://developers.google.com/apps-script/reference/script/authorization-info).

#### Example

The following example shows how to use `getAuthorizationInfo()` to skip features
where users haven't granted the required scopes. This allows the rest of the
execution flow to continue without prompting for authorization of the missing
scopes.

    // This function uses the Gmail scope and skips the email
    // capabilities if the scope for Gmail hasn't been granted.
    function myFunction() {
      const authInfo = ScriptApp.getAuthorizationInfo(ScriptApp.AuthMode.FULL, ['https://mail.google.com/']);
      if (authInfo.getAuthorizationStatus() === ScriptApp.AuthorizationStatus.NOT_REQUIRED) {
        GmailApp.sendEmail("dana@example.com", "Subject", "Body");
        Logger.log("Email sent successfully!");
      } else {
        const scopesGranted = ScriptApp.getAuthorizationInfo(ScriptApp.AuthMode.FULL).getAuthorizedScopes();
        console.warn(`Authorized scopes: ${scopesGranted} not enough to send mail, skipping.`);
      }
      // Continue the rest of the execution flow...
    }

### Ensure that trigger executions have permissions

Functions associated with triggers run automatically, and users might not be
present to provide permissions. We recommend that you use
[`requireScopes(authMode, oAuthScopes)`](https://developers.google.com/apps-script/reference/script/script-app#requirescopesauthmode,-oauthscopes)
before installing a trigger. This prompts the user for missing permissions
and doesn't allow the installation of the trigger without them.

#### Example

    // This function requires scope Sheets.
    function trackFormSubmissions(e){
      // Opens a spreadsheet to track the sent email.
      const ss = SpreadsheetApp.openById("abc1234567");
      const sheet = ss.getSheetByName("Submission Tracker")

      // Gets the last row of the sheet.
      const lastRow = sheet.getLastRow();

      // Adds email address of user that submitted the form
      // to column E of the last row of the spreadsheet.
      sheet.getRange(lastRow, 5).setValue(e.name);
      Logger.log("Sheet updated successfully!");
    }

    function installTrigger(){
      // Validates that the user has granted permissions for trigger
      // installation and execution. If not, trigger doesn't get
      // installed and prompts the user for authorization.
      ScriptApp.requireScopes(ScriptApp.AuthMode.FULL, [
        'https://www.googleapis.com/auth/script.scriptapp',
        'https://www.googleapis.com/auth/spreadsheets',
        'https://www.googleapis.com/auth/forms.currentonly'
      ]);
      ScriptApp.newTrigger('trackFormSubmission')
        .forForm(FormApp.getActiveForm())
        .onFormSubmit()
        .create();
    }

## OAuth verification

Certain OAuth scopes are *sensitive* because they allow access to Google
User Data. If your script project uses scopes that allow access to user data,
the project must go through
[OAuth client verification](https://developers.google.com/apps-script/guides/client-verification) before
you can publish it publicly as a web app or
[add-on](https://developers.google.com/workspace/add-ons/overview). For more
information, see the following guides:

- [OAuth client verification for Apps Script](https://developers.google.com/apps-script/guides/client-verification)
- [Unverified apps](https://support.google.com/cloud/answer/7454865)
- [OAuth verification FAQ](https://support.google.com/cloud/answer/9110914)
- [Google APIs Service: User Data Policy](https://developers.google.com/terms/api-services-user-data-policy)

## Restricted scopes

In addition to sensitive scopes, certain scopes are classified as
[*restricted*](https://support.google.com/cloud/answer/9110914#restricted-scopes)
and subject to additional rules that help protect user data. If you publish an
app that uses restricted scopes, it must comply with all specifications.

Review the [full list of restricted scopes](https://support.google.com/cloud/answer/9110914#restricted-scopes)
before publishing. Compliant apps must follow the
[Additional Requirements for Specific API scopes](https://developers.google.com/terms/api-services-user-data-policy#additional_requirements_for_specific_api_scopes).

Avoid using restricted scopes if possible to simplify the review process. You
can use restricted scopes freely for non-public apps.