# Scopes

Users must authorize add-ons and other applications that access their data or act on their behalf. When a user runs an add-on for the first time, the add-on UI presents an authorization prompt to start the authorization flow.

During this flow, the prompt tells the user what the application wants permission to do. For example, an add-on might want permission to read a user's email message or create events in their calendar. The add-on's script project defines these individual permissions as *OAuth scopes*.

You declare scopes in your [manifest](/workspace/add-ons/concepts/workspace-manifests) using URL strings. During the authorization flow, Apps Script presents a human-readable description of the scope to the user. For example, your Google Workspace add-on might use the "Read current message" scope, which is written in your manifest as `https://www.googleapis.com/auth/gmail.addons.current.message.readonly`. During the authorization flow, an add-on with this scope asks the user to allow the add-on to: **View your email messages when the add-on is running**.

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

You can explicitly set the scopes your script project uses by editing its [manifest](/workspace/add-ons/concepts/workspace-manifests) file. The manifest field [`oauthScopes`](/apps-script/manifest#Manifest.FIELDS.oauthScopes) is an array of all scopes used by the add-on. To set your project's scopes, do the following:

1. View the scopes your add-on uses. Determine what changes need to be made, such as using a narrower scope.
2. [Open your add-on's manifest file](/workspace/add-ons/concepts/workspace-manifests#editing_a_manifest).
3. Locate the top-level field labeled `oauthScopes`. If it is not present, you can add it.
4. The [`oauthScopes`](/apps-script/manifest#Manifest.FIELDS.oauthScopes) field specifies an array of strings. To set the scopes your project uses, replace the contents of this array with the scopes you want it to use. For example, for a Google Workspace add-on that extends Gmail you might have the following: ` { ... "oauthScopes": [ "https://www.googleapis.com/auth/gmail.addons.current.message.metadata", "https://www.googleapis.com/auth/userinfo.email" ], ... } `
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

## Choose scopes for Google Workspace add-ons

The following sections provide scopes that are commonly used for Google Workspace add-ons.

### Editor scopes

The following frequently-used scopes for Google Workspace add-ons extend Google Docs, Google Sheets, and Google Slides.

> **Note:** The `currentonly` scope is only available within Apps Script Services. This does not include Apps Script [Advanced Services](/apps-script/guides/services/advanced) or direct calls to Google Workspace APIs.

| Scope |  |
| --- | --- |
| Current Docs file access | `https://www.googleapis.com/auth/documents.currentonly` **Required if the add-on accesses the Google Apps Script Docs API.** Grants temporary access to the open document's content. |
| Current Sheets file access | `https://www.googleapis.com/auth/spreadsheets.currentonly` **Required if the add-on accesses the Apps Script Sheets API.** Grants temporary access to the open spreadsheet's content. |
| Current Slides file access | `https://www.googleapis.com/auth/presentations.currentonly` **Required if the add-on accesses the Apps Script Slides API.** Grants temporary access to the open presentation's content. |
| Per-file access | `https://www.googleapis.com/auth/drive.file` **Required for the add-on to use [`onFileScopeGrantedTrigger`](/apps-script/manifest/editor-addons#onfilescopegrantedtrigger) and if the add-on accesses Docs, Sheets, Slides, or Drive API**. Grants per-file access to files created or opened by the app using the Apps Script [Advanced Google Drive Service](/apps-script/advanced/drive). This doesn't allow similar actions using the basic [Drive service](/apps-script/reference/drive). File authorization is granted on a per-file basis and is revoked when the user deauthorizes the app. |

### Gmail

There are scopes created specifically for Google Workspace add-ons to help protect user Gmail data. Add these scopes explicitly to your add-on manifest, along with any others required.

The following table lists frequently-used scopes for Google Workspace add-ons that extend Gmail. If your add-on extends Gmail, you must add any scopes labeled **Required** to your Google Workspace add-on manifest.

Replace the broad `https://mail.google.com` scope with a narrower set of scopes that allow the interactions your add-on needs.

| Scope |  |
| --- | --- |
| Create new drafts | `https://www.googleapis.com/auth/gmail.addons.current.action.compose` **Required if the add-on uses [compose action triggers](/workspace/add-ons/gmail/extending-compose-ui#compose_trigger_function).** Allows the add-on to temporarily create new drafts messages and replies. See [Composing draft messages](/workspace/add-ons/gmail/compose) for details; this scope is often used with [compose actions] (/workspace/add-ons/gmail/extending-compose-ui). Requires an access token. |
| Read open message metadata | `https://www.googleapis.com/auth/gmail.addons.current.message.metadata` Grants temporary access to the open message's metadata (such as the subject or recipients). Doesn't allow reading of message content and requires an access token. **Required if the add-on uses metadata in compose action triggers.** For [compose actions](/workspace/add-ons/gmail/extending-compose-ui), this scope is required if a compose trigger needs access to metadata. In practice, this scope lets a compose trigger access recipient lists (to:, cc:, and bcc:) of a reply email draft. |
| Read open message content | `https://www.googleapis.com/auth/gmail.addons.current.message.action` Grants access to the open message's content upon user interaction, such as when selecting an add-on menu item. Requires an access token. |
| Read open thread content | `https://www.googleapis.com/auth/gmail.addons.current.message.readonly` Grants temporary access to the open message's metadata and content. Also grants access to the content of other messages in the open thread. Requires an access token. |
| Read any message content and metadata | `https://www.googleapis.com/auth/gmail.readonly` Read any email metadata and content, including the open message. Required if you need to read information about other messages, such as when conducting a search query or reading an entire mail thread. **Warning**: This is a very broad, restricted scope. Only use it if absolutely necessary. |

### Google Calendar scopes

The following table lists frequently-used scopes for Google Workspace add-ons that extend Google Calendar.

| Scope |  |
| --- | --- |
| Access event metadata | `https://www.googleapis.com/auth/calendar.addons.execute` **Required if the add-on accesses Calendar event metadata.** Allows the add-on to access event metadata. |
| Read user-generated event data | `https://www.googleapis.com/auth/calendar.addons.current.event.read` **Required if the add-on needs to read user-generated event data.** Allows the add-on to access user-generated event data. This data is only available if the [`addOns.calendar.eventAccess` manifest field](/apps-script/manifest/calendar-addons) is set to `READ` or `READ_WRITE`. |
| Write user-generated event data | `https://www.googleapis.com/auth/calendar.addons.current.event.write` **Required if the add-on needs to write user-generated event data.** Allows the add-on to edit user-generated event data. This data is only available if the [`addOns.calendar.eventAccess` manifest field](/apps-script/manifest/calendar-addons) is set to `WRITE` or `READ_WRITE`. |

### Google Chat scopes

To call the Google Chat API, authenticate as the [Google Chat user](/workspace/chat/authenticate-authorize-chat-user) or as the [Google Chat app](/workspace/chat/authenticate-authorize-chat-app). Each type of authentication requires different scopes, and not all Chat API methods support app authentication.

To learn more about Chat scopes and authentication types, see the Chat API [Authentication and authorization overview](/workspace/chat/authenticate-authorize)

The following table shows frequently-used Chat API methods and scopes based on the supported authentication types:

| Method | [User authentication](/chat/api/guides/auth/users) supported | [App authentication](/chat/api/guides/auth/service-accounts) supported | Authorization scopes supported |  |
| --- | --- | --- | --- | --- |
| [Send a message](/chat/api/guides/v1/messages/create) | check | check | With [User authentication](/chat/api/guides/auth/users): `chat.messages.create` `chat.messages` `chat.import` With [App authentication](/chat/api/guides/auth/service-accounts): `chat.bot` |  |
| [Create a space](/chat/api/guides/v1/spaces/create) | check | check | With [User authentication](/chat/api/guides/auth/users): `chat.spaces.create` `chat.spaces` `chat.import` With [App authentication](/chat/api/guides/auth/service-accounts) and [administrator approval](https://support.google.com/a?p=chat-app-auth) (available in [Developer Preview](/workspace/preview)): `chat.app.spaces.create` `chat.app.spaces` |  |
| [Create and add members to a space](/chat/api/guides/v1/spaces/set-up) | check | — | With [User authentication](/chat/api/guides/auth/users): `chat.spaces.create` `chat.spaces` |  |
| [Add a user to a space](/chat/api/guides/v1/members/create) | check | check | With [User authentication](/chat/api/guides/auth/users): `chat.memberships` `chat.memberships.app` `chat.import` With [App authentication](/chat/api/guides/auth/service-accounts) and [administrator approval](https://support.google.com/a?p=chat-app-auth) (available in [Developer Preview](/workspace/preview)): `chat.app.memberships` |  |
| [List activities or events from a Chat space](/chat/api/reference/rest/v1/spaces.spaceEvents/list) | check | — | With [User authentication](/chat/api/guides/auth/users), you must use a scope for each [event type](/workspace/chat/api/reference/rest/v1/spaces.spaceEvents#SpaceEvent.FIELDS.event_type) included in the request: For events about messages: `chat.messages` `chat.messages.readonly` For events about reactions: `chat.messages.reactions` `chat.messages.reactions.readonly` `chat.messages` `chat.messages.readonly` For events about memberships: `chat.memberships` `chat.memberships.readonly` For events about the space: `chat.spaces` `chat.spaces.readonly` |  |

### Google Drive scopes

The following table lists frequently-used scopes for Google Workspace add-ons that extend Google Drive.

| Scope |  |
| --- | --- |
| Read selected item metadata | `https://www.googleapis.com/auth/drive.addons.metadata.readonly` **Required if the add-on implements a contextual interface triggered when the user selects items in Drive.** Allows the add-on to read limited metadata about items a user has selected in Google Drive. The metadata is limited to the item's ID, title, MIME type, icon URL and whether the add-on has permission to access the item. |
| Per-file access | `https://www.googleapis.com/auth/drive.file` **Recommended if the add-on needs to access individual Drive files.** Grants per-file access to files created or opened by the app using the Apps Script [Advanced Drive Service](/apps-script/advanced/drive). This doesn't allow similar actions using the basic [Drive service](/apps-script/reference/drive). File authorization is granted on a per-file basis and is revoked when the user deauthorizes the app. See the [Request file access for selected files example](/workspace/add-ons/drive/drive-actions#request_file_access_for_selected_files). |

#### Access tokens

To protect user data, the Gmail scopes used in Google Workspace add-ons grant temporary access to user data. To enable temporary access, call [`GmailApp.setCurrentMessageAccessToken`](/apps-script/reference/gmail/gmail-app#setcurrentmessageaccesstokenaccesstoken) using an access token from an [action event object](/workspace/add-ons/concepts/actions#action_event_objects).

The access token that enables Gmail scopes isn't the same as the access token returned by `ScriptApp.getOAuthToken`. Use the token provided in the action event object.

The following shows an example of setting an access token to allow access to a message's metadata. The only scope necessary for this example is `https://www.googleapis.com/auth/gmail.addons.current.message.metadata`.

```
function readSender(e) {
  var accessToken = e.gmail.accessToken;
  var messageId = e.gmail.messageId;

  // The following function enables short-lived access to the current
  // message in Gmail. Access to other Gmail messages or data isn't
  // permitted.
  GmailApp.setCurrentMessageAccessToken(accessToken);
  var mailMessage = GmailApp.getMessageById(messageId);
  return mailMessage.getFrom();
}
```

### Other Google Workspace scopes

Your add-on may require additional scopes if it uses other Google Workspace or Apps Script services. In most cases, Apps Script detects these scopes and updates the manifest automatically. When editing your manifest's scope list, don't remove any scopes unless you are replacing them with a narrower alternative.

The following table shows scopes that Google Workspace add-ons often use:

| Scope |  |
| --- | --- |
| Read user's email address | `https://www.googleapis.com/auth/userinfo.email` Allows the project to read the current user's email address. |
| Allow calls to external services | `https://www.googleapis.com/auth/script.external_request` Allows the project to make [`UrlFetch`](/apps-script/reference/url-fetch) requests. This is also required if the project makes use of the [OAuth2 for Apps Script](https://github.com/googlesamples/apps-script-oauth2) library. |
| Read user's locale and timezone | `https://www.googleapis.com/auth/script.locale` Allows the project to learn the current user's locale and timezone. See [Accessing user locale and timezone](/workspace/add-ons/how-tos/access-user-locale) for details. |
| Create triggers | `https://www.googleapis.com/auth/script.scriptapp` Allows the project to create [triggers](/apps-script/guides/triggers/installable#managing_triggers_programmatically). |
| Preview third-party links | `https://www.googleapis.com/auth/workspace.linkpreview` **Required if the add-on previews links from a third-party service.** Allows the project to see a link within a Google Workspace application while the user is interacting with it. To learn more, see [Preview links with smart chips](/workspace/add-ons/editors/gsao/preview-links). |
| Create third-party resources | `https://www.googleapis.com/auth/workspace.linkcreate` **Required if the add-on creates resources in a third-party service.** Allows the project to read the information that users submit to the resource creation form and insert a link to the resource within a Google Workspace application. To learn more, see [Create third-party resources from the @ menu](/workspace/add-ons/editors/gsao/create-insert-resource-smart-chip). |
