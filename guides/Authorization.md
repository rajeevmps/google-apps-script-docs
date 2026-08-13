# Authorization for Google Services

Google Apps Script requires user authorization to access private data from
[built-in Google services](https://developers.google.com/apps-script/guides/services) or
[advanced Google services](https://developers.google.com/apps-script/guides/services/advanced).

## How authorization for Google Services works

When a script requires access to Google services, it follows this general
process:

1. **Detection** : Apps Script scans the script to identify which services it uses (for example, `SpreadsheetApp` or `GmailApp`).
2. **Scope determination** : Based on the scan, Apps Script identifies a set of [OAuth scopes](https://developers.google.com/apps-script/concepts/scopes) needed for the script to run.
3. **Authorization check**: When the script is run, it checks if the user has already authorized those scopes.
4. **User prompt**: If authorization is missing, a dialog appears asking the user to grant permission.
5. **Execution**: After the script is authorized, it can access the requested data for that user.

## Permissions and types of scripts

The user identity that a script runs with --- and thus the data it can access ---
varies based on the scenario in which the script is run, as shown in the
following table.

| Type of script | Script runs as... |
|---|---|
| [Standalone](https://developers.google.com/apps-script/execution_script_editor), [Google Workspace add-on](https://developers.google.com/workspace/add-ons/overview), or [bound to Google Docs, Google Sheets, Google Slides, or Google Forms](https://developers.google.com/apps-script/guides/bound) | User at the keyboard |
| [Custom function in a spreadsheet](https://developers.google.com/apps-script/execution_custom_functions) | [Anonymous user](https://developers.google.com/apps-script/execution_custom_functions#permissions); however, [quota limits](https://developers.google.com/apps-script/guides/services/quotas) count against user at the keyboard |
| [Web app](https://developers.google.com/apps-script/execution_web_apps) or [Google Sites gadget](https://developers.google.com/apps-script/execution_gadgets) | User at the keyboard or script owner, dependent on [options selected](https://developers.google.com/apps-script/execution_web_apps#permissions) when deploying the app |
| [Installable trigger](https://developers.google.com/apps-script/understanding_triggers#Installable) | User who created the trigger |

## Grant access rights

![](https://developers.google.com/static/apps-script/images/new-auth-1.png) ![](https://developers.google.com/static/apps-script/images/new-auth-2.png)

Apps Script determines the authorization scopes (like access to
your Sheets
files or Gmail) automatically, based on a scan of the code. Code
that is commented out can still generate an authorization request. If a script
needs authorization, an authorization dialog appears when it is run.

Scripts that you have previously authorized also ask for additional
authorization if a code change adds new services. Scripts may not request
authorization if you access the script as a web app that runs under
[the script owner's user identity](https://developers.google.com/apps-script/execution_web_apps#permissions).

> [!WARNING]
> **Warning:** Web apps and other scripts that use sensitive scopes are subject to review by Google. Users attempting to authorize such apps may see a warning screen saying the app is *unverified* by Google. See [OAuth client verification](https://developers.google.com/apps-script/guides/client-verification) for details.

## Revoke access rights

To revoke a script's access to your data, follow these steps:

1. Visit the [Security section of your Google
   Account](https://myaccount.google.com/security).
2. Under **Your connections to third-party apps \& services** , click **See all
   connections**.
3. Select the script or app you want to revoke access for.
4. Click **Delete all connections you have with <var translate="no">APP_NAME</var>** , then click **Confirm**.

## Limit scope to the current document

If you're building an
[add-on](https://developers.google.com/workspace/add-ons/overview) or other script
that uses the [Spreadsheet service](https://developers.google.com/apps-script/reference/spreadsheet),
[Document service](https://developers.google.com/apps-script/reference/document),
[Slides service](https://developers.google.com/apps-script/reference/slides), or
[Forms service](https://developers.google.com/apps-script/reference/forms), you can force the authorization
dialog to ask only for access to files in which the add-on or script is used,
rather than all of a user's spreadsheets, documents, or forms. To do so, include
the following [JSDoc](https://developers.google.com/apps-script/concepts/jsdoc) annotation in a file-level comment:

    /**
     * @OnlyCurrentDoc
     */

An opposing annotation, `@NotOnlyCurrentDoc`, is available if your script
includes a [library](https://developers.google.com/apps-script/guides/libraries) that declares
`@OnlyCurrentDoc`, but the primary script actually requires access to more than
the current file.

## Authorization lifecycle for add-ons

[Add-ons](https://developers.google.com/workspace/add-ons/overview) for Sheets,
Docs, Slides, and Forms
generally follow the same authorization model as scripts that are
[bound](https://developers.google.com/apps-script/guides/bound) to a document. In certain
circumstances, however, their `onOpen(e)` and `onEdit(e)` functions run in a
no-authorization mode that presents some additional complications. For more
information, see the
[guide to the add-ons authorization lifecycle](https://developers.google.com/workspace/add-ons/concepts/addon-authorization#editor_add-on_authorization).

## OAuth application user limits

Applications that use OAuth to access Google user data, including Apps
Script projects, are subject to authorization limits. See
[OAuth application user limits](https://support.google.com/cloud/answer/9028764)
for details.

## Re-authentication behavior with Apps Script

Apps Script does not enforce the
[re-authentication frequency](https://support.google.com/a/answer/9368756) that
is configured in Google Cloud service settings. This is because
Apps Script can run automatically using triggers, which operate
without direct user interaction. These automated executions don't trigger the
re-authentication prompts. Your Apps Script application doesn't
automatically ask you to re-authenticate after the specified time period
(for example, 12 hours).

## Set explicit scopes in the manifest

Apps Script automatically determines required scopes by scanning
the code for function calls. If you need more control, you can explicitly set
the scopes in the project manifest (`appsscript.json`). This is recommended for
published scripts to ensure that you're using the minimum required permissions.

For instructions, see [Set explicit scopes](https://developers.google.com/apps-script/concepts/scopes#set-explicit).

## Troubleshooting

- **"Authorization required" error when running a trigger**: Triggers must be authorized by the user who created them. If you add code that requires new permissions, you must manually run a function in the script editor once to trigger the authorization dialog.
- **Scopes not updating** : If you've updated your code but the authorization dialog doesn't reflect the changes, try saving the project and refreshing the editor. If you are using explicit scopes in the manifest, ensure you've added the new scope to the `oauthScopes` array.
- **"This app is blocked" or unverified app warning** : This occurs if your script uses sensitive or restricted scopes and hasn't been verified by Google. See [OAuth client verification](https://developers.google.com/apps-script/guides/client-verification).