# ScriptApp

Access and manipulate script publishing and triggers.

Access and manipulate script publishing and triggers. This class allows users to create script triggers and control publishing the script as a service.

## Properties

| Property | Type | Description |
|----------|------|-------------|
| `AuthMode` | `AuthMode` | An enumeration that identifies which categories of authorized services Apps Script is able to execute through a triggered function. |
| `AuthorizationStatus` | `AuthorizationStatus` | An enumeration denoting the authorization status of a script. |
| `EventType` | `EventType` | An enumeration denoting the type of triggered event. |
| `InstallationSource` | `InstallationSource` | An enumeration denoting how the script was installed to the user as an add-on. |
| `TriggerSource` | `TriggerSource` | An enumeration denoting the source of the event that causes the trigger to fire. |
| `WeekDay` | `Weekday` | An enumeration representing the days of the week. |

## Methods

### deleteTrigger(trigger: Trigger) → void

Removes the given trigger so it no longer runs.

**Parameters:**
- `trigger` (`Trigger`): The trigger to delete.

**Authorization:** Requires the scope `https://www.googleapis.com/auth/script.scriptapp`.

```javascript
const triggers = ScriptApp.getProjectTriggers();
for (let i = 0; i < triggers.length; i++) {
  ScriptApp.deleteTrigger(triggers[i]);
}
```

### getAuthorizationInfo(authMode: AuthMode) → AuthorizationInfo

Gets an object that checks if the user has granted authorization for all the script requirements. The object also provides an authorization URL for users to grant those permissions, in case any of the script requirements are not authorized.

Some script executions can start without a user's consent for all required scopes used by the script. The information in this object lets you control access to sections of code that require certain scopes and request authorization of those scopes for subsequent executions.

**Parameters:**
- `authMode` (`AuthMode`): The authorization mode for which authorization information is requested; in almost all cases, the value for `authMode` should be `ScriptApp.getAuthorizationInfo(ScriptApp.AuthMode.FULL)`, since no other authorization mode requires that users grant authorization.

**Return:** `AuthorizationInfo` — An object that can provide information about the user's authorization status.

```javascript
const authInfo = ScriptApp.getAuthorizationInfo(ScriptApp.AuthMode.FULL);
const status = authInfo.getAuthorizationStatus();
const url = authInfo.getAuthorizationUrl();
```

### getAuthorizationInfo(authMode: AuthMode, oAuthScopes: String[]) → AuthorizationInfo

Gets an object that checks if the user has granted authorization for the requested scopes. The object also provides an authorization URL for users to grant those permissions, in case any of the requested scopes are not authorized.

Some script executions can start without a user's consent for all required scopes used by the script. The information in this object lets you control access to sections of code that require certain scopes and request authorization of those scopes for subsequent executions. Scopes that are invalid or not required by the script lead to an error.

**Parameters:**
- `authMode` (`AuthMode`): The authorization mode for which authorization information is requested; in almost all cases, the value for `authMode` should be `ScriptApp.AuthMode.FULL`, since no other authorization mode requires that users grant authorization.
- `oAuthScopes` (`String[]`): The OAuth scopes for which authorization information is requested.

**Return:** `AuthorizationInfo` — An object that provides information about the user's authorization status and an authorization URL in case some consents are missing.

```javascript
const authInfo = ScriptApp.getAuthorizationInfo(ScriptApp.AuthMode.FULL, [
  'https://www.googleapis.com/auth/documents',
  'https://www.googleapis.com/auth/presentations',
]);
const status = authInfo.getAuthorizationStatus();
const url = authInfo.getAuthorizationUrl();
```

### getIdentityToken() → String|null

Gets an OpenID Connect identity token for the effective user, if the `openid` scope has been granted. This scope is not included by default, and you must add it as an explicit scope in the manifest file to request it. Include the scopes `https://www.googleapis.com/auth/userinfo.email` or `https://www.googleapis.com/auth/userinfo.profile` to return additional user information in the token.

The returned ID token is an encoded JSON Web Token (JWT), and it must be decoded to extract information from it. The following examples shows how to decode the token and extract the effective user's Google profile ID.

**Return:** `String|null` — The identity token if available; otherwise `null`.

```javascript
const idToken = ScriptApp.getIdentityToken();
const body = idToken.split('.')[1];
const decoded = Utilities
                    .newBlob(
                        Utilities.base64Decode(body),
                        )
                    .getDataAsString();
const payload = JSON.parse(decoded);

Logger.log(`Profile ID: ${payload.sub}`);
```

### getInstallationSource() → InstallationSource

Returns an enum value that indicates how the script came to be installed as an add-on for the current user (for example, whether the user installed it personally through the Chrome Web Store, or whether a domain administrator installed it for all users).

**Return:** `InstallationSource` — The source of installation.

### getOAuthToken() → String

Gets the OAuth 2.0 access token for the effective user. If the script's OAuth scopes are sufficient to authorize another Google API that normally requires its own OAuth flow (like Google Picker), scripts can bypass the second authorization prompt by passing this token instead. The token expires after a time (a few minutes at minimum); scripts should handle authorization failures and call this method to obtain a fresh token when needed.

The token returned by this method only includes scopes that the script currently needs. Scopes that were previously authorized but are no longer used by the script are not included in the returned token. If additional OAuth scopes are needed beyond what the script itself requires, they can be specified in the script's manifest file.

You can use this method to call Google APIs that Apps Script doesn't directly support. Pass the returned token in the `Authorization` header of an HTTP request using `UrlFetchApp.fetch(url, params)`.

**Return:** `String` — A string representation of the OAuth 2.0 token.

```javascript
const url = 'https://www.googleapis.com/drive/v3/files';
const method = 'GET';
const headers = {
  Authorization: 'Bearer ' + ScriptApp.getOAuthToken(),
};
const response = UrlFetchApp.fetch(url, {
  method,
  headers,
});
```

### getProjectTriggers() → Trigger[]

Gets all installable triggers associated with the current project and current user.

**Return:** `Trigger[]` — An array of the current user's triggers associated with this project.

**Authorization:** Requires the scope `https://www.googleapis.com/auth/script.scriptapp`.

```javascript
Logger.log(
    `Current project has ${ScriptApp.getProjectTriggers().length} triggers.`,
);
```

### getScriptId() → String

Gets the script project's unique ID. This is the preferred method to get the unique identifier for the script project as opposed to `getProjectKey()`. This ID can be used in all places where project key was previously provided.

**Return:** `String` — The script project's ID.

### getService() → Service

Gets an object used to control publishing the script as a web app.

**Return:** `Service` — An object used to observe and control publishing the script as a web app.

```javascript
const url = ScriptApp.getService().getUrl();
```

### getUserTriggers(document: Document) → Trigger[]

Gets all installable triggers owned by this user in the given document, for this script or add-on only. This method cannot be used to see the triggers attached to other scripts.

**Parameters:**
- `document` (`Document`): A Google Docs file that may contain installable triggers.

**Return:** `Trigger[]` — An array of triggers owned by this user in the given document.

**Authorization:** Requires the scope `https://www.googleapis.com/auth/script.scriptapp`.

```javascript
const doc = DocumentApp.getActiveDocument();
const triggers = ScriptApp.getUserTriggers(doc);
Logger.log(triggers[0].getHandlerFunction());
```

### getUserTriggers(form: Form) → Trigger[]

Gets all installable triggers owned by this user in the given form, for this script or add-on only. This method cannot be used to see the triggers attached to other scripts.

**Parameters:**
- `form` (`Form`): A Google Forms file that may contain installable triggers.

**Return:** `Trigger[]` — An array of triggers owned by this user in the given form.

**Authorization:** Requires the scope `https://www.googleapis.com/auth/script.scriptapp`.

```javascript
const form = FormApp.getActiveForm();
const triggers = ScriptApp.getUserTriggers(form);
Logger.log(triggers[0].getTriggerSource());
```

### getUserTriggers(spreadsheet: Spreadsheet) → Trigger[]

Gets all installable triggers owned by this user in the given spreadsheet, for this script or add-on only. This method cannot be used to see the triggers attached to other scripts.

**Parameters:**
- `spreadsheet` (`Spreadsheet`): A Google Sheets file that may contain installable triggers.

**Return:** `Trigger[]` — An array of triggers owned by this user in the given spreadsheet.

**Authorization:** Requires the scope `https://www.googleapis.com/auth/script.scriptapp`.

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const triggers = ScriptApp.getUserTriggers(ss);
Logger.log(triggers[0].getEventType());
```

### invalidateAuth() → void

Invalidates the authorization the effective user has to execute the current script. Used to invalidate any permissions for the current script. This is especially useful for functions tagged as one-shot authorization. Since one-shot authorization functions can only be called the first run after the script has acquired authorization, if you wish to perform an action afterwards, you must revoke any authorization the script had, so the user can see the authorization dialog again.

**Throws:** `Error` when invalidation fails.

```javascript
ScriptApp.invalidateAuth();
```

### newStateToken() → StateTokenBuilder

Creates a builder for a state token that can be used in a callback API (like an OAuth flow).

**Return:** `StateTokenBuilder` — An object used to continue the state-token-building process.

```javascript
function getCallbackURL(callbackFunction) {
  const scriptUrl =
      'https://script.google.com/macros/d/1234567890abcdefghijklmonpqrstuvwxyz';
  const urlSuffix = '/usercallback?state=';
  const stateToken = ScriptApp.newStateToken()
                         .withMethod(callbackFunction)
                         .withTimeout(120)
                         .createToken();
  return scriptUrl + urlSuffix + stateToken;
}
```

### newTrigger(functionName: String) → TriggerBuilder

Begins the process of creating an installable trigger that, when fired, calls a given function.

Before creating a trigger, verify that the associated function has all the necessary OAuth permissions.

**Parameters:**
- `functionName` (`String`): The function to call when the trigger fires. You can use functions from included libraries, such as `Library.libFunction1`.

**Return:** `TriggerBuilder` — An object used to continue the trigger-building process.

**Authorization:** Requires the scope `https://www.googleapis.com/auth/script.scriptapp`.

```javascript
ScriptApp.newTrigger('myFunction')
    .forSpreadsheet('1234567890abcdefghijklmnopqrstuvwxyz_a1b2c3')
    .onEdit()
    .create();
```

### requireAllScopes(authMode: AuthMode) → void

Validates if the user has granted consent for all of the scopes requested by the script. Use this method if an execution flow relies on all of the scopes that a script requests. If any consents are missing, then this method ends the current execution and renders an authorization prompt to request the missing consents.

This method only works when users run the script from a surface that supports granular consent, for example, from within the Apps Script IDE. When the script is run with missing consents from an unsupported surface, such as a Google Workspace add-on, the script renders an authorization prompt at the start of the execution to request all the scopes.

**Parameters:**
- `authMode` (`AuthMode`): The authorization mode for which script scopes needs to be evaluated, in almost all cases, the value for `authMode` should be `ScriptApp.AuthMode.FULL`, since no other authorization mode requires that users grant authorization.

```javascript
ScriptApp.requireAllScopes(ScriptApp.AuthMode.FULL);
```

### requireScopes(authMode: AuthMode, oAuthScopes: String[]) → void

Validates if the user has granted consent for the requested scopes. Use this method if an execution flow relies on one or more services. If any of the specified consents are missing, then this method ends the current execution and renders an authorization prompt to request the missing consents. Scopes that are invalid or not required by the script lead to an error.

This method only works when users run the script from a surface that supports granular consent, for example, from within the Apps Script IDE. When the script is run with missing consents from an unsupported surface, such as a Google Workspace add-on, the script renders an authorization prompt at the start of the execution to request all the scopes.

**Parameters:**
- `authMode` (`AuthMode`): The authorization mode for which requested scopes needs to be evaluated, in almost all cases, the value for `authMode` should be `ScriptApp.AuthMode.FULL`, since no other authorization mode requires that users grant authorization.
- `oAuthScopes` (`String[]`): The OAuth scopes that are required to complete the given execution flow.

```javascript
ScriptApp.requireScopes(ScriptApp.AuthMode.FULL, [
  'https://www.googleapis.com/auth/documents',
  'https://www.googleapis.com/auth/presentations',
]);
```

## Deprecated Methods

### getProjectKey() → String *(Deprecated: use `getScriptId()` instead)*

Gets the project key of the current script. The project key is a unique identifier for scripts and used to compose the callback URL used in conjunction with `newStateToken()`.

When called in a library, this returns the project key of the outer-most script being executed.

**Return:** `String` — The project key of the current script.

### getScriptTriggers() → Trigger[] *(Deprecated)*

This function is deprecated and should not be used in new scripts.

Gets all installable triggers associated with the current project and current user.

**Return:** `Trigger[]` — An array of the current user's triggers associated with this project.

```javascript
Logger.log(
    `Current script has ${ScriptApp.getScriptTriggers().length} triggers.`,
);
```
