# AuthorizationInfo

An object that checks if the user has granted authorization for the required scopes of the script.

An object that checks if the user has granted authorization for the required scopes of the script. The object also provides an authorization URL for users to grant those permissions.

Some script executions can start without a user's consent to all required scopes used by the script. The information in this object lets you control access to sections of code that require certain scopes and request authorization of those scopes for subsequent executions.

This object is returned by `ScriptApp.getAuthorizationInfo(authMode)`. In almost all cases, scripts should call `ScriptApp.getAuthorizationInfo(ScriptApp.AuthMode.FULL)`, since no other authorization mode requires that users grant authorization.

## Methods

### getAuthorizationStatus() → AuthorizationStatus

Gets a value that indicates whether the user needs to authorize this script to use one or more services (for example, `ScriptApp.AuthorizationStatus.REQUIRED`).

**Return:** `AuthorizationStatus` — The authorization status.

```javascript
const authInfo = ScriptApp.getAuthorizationInfo(ScriptApp.AuthMode.FULL);
Logger.log(authInfo.getAuthorizationStatus());
```

### getAuthorizationUrl() → String|null

Gets the authorization URL that can be used to grant access to the script. This method returns `null` if no authorization is required. The page at the URL closes automatically if it is accessed and the script does not require any authorization.

**Return:** `String|null` — A URL that can be used to authorize the script.

```javascript
const authInfo = ScriptApp.getAuthorizationInfo(ScriptApp.AuthMode.FULL);
Logger.log(authInfo.getAuthorizationUrl());
```

### getAuthorizedScopes() → String[]|null

Gets a list of authorized scopes for the script. If authorization information is requested for a specified list of scopes, returns the authorized scopes from the specified list.

**Return:** `String[]|null` — The list of authorized scopes.

```javascript
const authInfo = ScriptApp.getAuthorizationInfo(ScriptApp.AuthMode.FULL, [
  'https://www.googleapis.com/auth/documents',
  'https://www.googleapis.com/auth/spreadsheets',
]);
Logger.log(authInfo.getAuthorizedScopes());
```
