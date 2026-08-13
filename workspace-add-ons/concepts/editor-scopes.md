# Authorization scopes for Editor add-ons

Users must authorize add-ons and other applications that access their data or act on their behalf. When a user runs an add-on for the first time, the add-on UI presents an authorization prompt to start the authorization flow.

During this flow, the prompt tells the user what the application wants permission to do. For example, an add-on might want permission to read a user's email message or create events in their calendar. The add-on's script project defines these individual permissions as *OAuth scopes*.

You declare scopes in your [manifest](/workspace/add-ons/concepts/editor-manifests) using URL strings. During the authorization flow, Apps Script presents a human-readable description of the scope to the user. For example, your add-on might use the "Read current document" scope, which is written in your manifest as `https://www.googleapis.com/auth/documents.currentonly`. During the authorization flow, an add-on with this scope asks the user to allow the add-on to: **View and manage documents that this application has been installed in.** **Note:** The `currentonly` scope is only available within Apps Script Services. This does not include Apps Script [Advanced Services](/apps-script/guides/services/advanced) or direct calls to Google Workspace APIs.

The scopes Apps Script uses for its various services overlap with the scopes used by the related API. For example, Apps Script's [Calendar service](/apps-script/reference/calendar) uses many of the same scopes as the [Calendar API](/workspace/calendar). You can look up the scopes that particular Apps Script service methods require in the Apps Script [reference documentation](/apps-script/reference).

## View scopes

You can see the scopes your script project currently requires by doing the following:

1. Open the script project.
2. At the left, click **Overview** info_outline.
3. View the scopes under "Project OAuth Scopes."

You can also view the script project's current scopes in the project manifest, under the [`oauthScopes`](/apps-script/manifest#Manifest.FIELDS.oauthScopes) field, but only if you have set those scopes explicitly.

## Set explicit scopes

Apps Script automatically determines what scopes a script needs by scanning its code for function calls that require them. For most scripts this is sufficient and saves you time, but for published add-ons you should exercise more direct control of the scopes.

For example, Apps Script might give an add-on script project the very permissive scope `https://mail.google.com` by default. When a user authorizes a script project with this scope, the project is granted full access to the user's Gmail account. For published add-ons, you **must** replace this scope with a more limited set that cover the add-ons's needs and no more.

> **Warning:** Always use the least permissive scope set possible. To protect user information, add-ons and other published applications should *never* ask for more scope permissions than they absolutely need. The scopes your add-on requires are examined during the publication [add-on review](/workspace/marketplace/about-app-review) process; if the add-on uses scopes that are too broad it can't pass review.

You can explicitly set the scopes your script project uses by editing its [manifest](/workspace/add-ons/concepts/editor-manifests) file. The manifest field [`oauthScopes`](/apps-script/manifest#Manifest.FIELDS.oauthScopes) is an array of all scopes used by the add-on. To set your project's scopes, do the following:

1. View the scopes your add-on uses. Determine what changes need to be made, such as using a narrower scope.
2. [Open your add-on's manifest file](/workspace/add-ons/concepts/editor-manifests#editing_a_manifest).
3. Locate the top-level field labeled `oauthScopes`. If it is not present, you can add it.
4. The [`oauthScopes`](/apps-script/manifest#Manifest.FIELDS.oauthScopes) field specifies an array of strings. To set the scopes your project uses, replace the contents of this array with the scopes you want it to use. For example, for an Editor add-on that extends Sheets you might have the following: ` { ... "oauthScopes": [ "https://www.googleapis.com/auth/script.container.ui", "https://www.googleapis.com/auth/spreadsheets" ], ... } `
5. Save the manifest file changes.

## OAuth verification

Using certain sensitive OAuth scopes may require that your add-on go through [OAuth client verification](/apps-script/guides/client-verification) before you can publish it. For more information, see the following guides:

- [OAuth client verification for Apps Script](/apps-script/guides/client-verification)
- [Unverified apps](https://support.google.com/cloud/answer/7454865)
- [OAuth verification FAQ](https://support.google.com/cloud/answer/9110914)
- [Google APIs Service: User Data Policy](/terms/api-services-user-data-policy)

## Restricted scopes

Certain scopes are *restricted* and subject to additional rules that help protect user data. If you intend to publish a Gmail or Editor add-on that uses one or more restricted scopes, the add-on must comply with all the specified restrictions before it can be published.

Review the [full list of restricted scopes](https://support.google.com/cloud/answer/9110914#restricted-scopes) before you attempt to publish. If your add-on uses any of them, you must comply with the [Additional requirements for specific API scopes](/terms/api-services-user-data-policy#additional-requirements-for-specific-api-scopes) prior to publishing.

> **Note:** Avoid using restricted scopes in your add-on if you can—it is easier to pass add-on review for public publication if you don't use them. You can use restricted scopes freely for non-public add-ons.

The [Google Workspace Developer Tools extension](https://marketplace.visualstudio.com/items?itemName=google-workspace.google-workspace-developer-tools) for Visual Studio Code provides diagnostic information for all scopes including the scope's description and whether it is sensitive or restricted.

## Editor add-on scopes

When you build an Editor add-on, the required scopes are determined by the Google Apps Script service and methods the add-on code uses. For example, a Google Sheets add-on might need the `https://www.googleapis.com/auth/spreadsheets.readonly` scope in order to read information from different Sheets.

Apps Script automatically determines the scopes required by the services you use as you add code to your script project. For Editor add-ons, you can often just rely on this automatic scope collection instead of determining the scopes yourself and setting them explicitly.

If you are not setting your scopes explicitly and your Editor add-on only ever reads or writes to the open editor file, add the following comment to one of your script project files:

```
/**
 * @OnlyCurrentDoc
 */
```

This comment tells Apps Script to narrow the editor file scopes it sets to `currentonly`. For example, if you add this comment to a Sheets add-on script project file, you are specifying that the add-on only needs permission to operate on the open Sheet, and not any other Sheets the user might have in Google Drive. Conversely, you shouldn't use this comment if your Sheets add-on needs to read or write data in a Sheet the user doesn't have open.

> **Note:** The `currentonly` scope is only available within Apps Script Services. This does not include Apps Script [Advanced Services](/apps-script/guides/services/advanced) or direct calls to Google Workspace APIs.
