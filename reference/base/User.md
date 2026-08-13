# User

Representation of a user, suitable for scripting.

Representation of a user, suitable for scripting.

## Methods

### getEmail() → String

Gets the user's email address, if available. If security policies do not allow access to the user's email address, this method returns a blank string. The circumstances in which the email address is available vary: for example, the user's email address is not available in any context that allows a script to run without that user's authorization, like a simple `onOpen(e)` or `onEdit(e)` trigger, a custom function in Google Sheets, or a web app deployed to "execute as me" (that is, authorized by the developer instead of the user). However, these restrictions generally do not apply if the developer runs the script themselves or belongs to the same Google Workspace domain as the user.

**Return:** The user's email's address, or a blank string if security policies do not allow access to the user's email address.

## Code Sample

```javascript
// Log the email address of the person running the script.
Logger.log(Session.getActiveUser().getEmail());
```

## Deprecated Methods

### getUserLoginId() → String

Deprecated. As of June 24, 2013, replaced by `getEmail()`.

Gets the user's email address.

**Return:** The user's email's address.
