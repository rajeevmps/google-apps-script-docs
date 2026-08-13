# Session

The Session class provides access to session information, such as the user's email address (in some circumstances) and language setting.

The Session class provides access to session information, such as the user's email address (in some circumstances) and language setting.

## Methods

### getActiveUser() → User

Gets information about the current user. If security policies do not allow access to the user's identity, User.getEmail() returns a blank string.

The email address is generally unavailable in the following scenarios: authorization scopes do not include an email-based scope like `https://www.googleapis.com/auth/userinfo.email`; the script executes as a trigger, such as `onOpen(e)` or `onEdit(e)`; the script is a custom function used in a spreadsheet cell; the script is a web app deployed to execute as a different user (e.g. "execute as me"). These restrictions generally do not apply if the developer running the script (or who set up the trigger) is the same user, or belongs to the same Google Workspace domain as the file owner.

**Return:** `User` — the current user

**Authorization:** Scripts that use this method require authorization with one or more of the following scopes: `https://www.googleapis.com/auth/userinfo.email`

**Code Sample:**
```javascript
// Log the email address of the person running the script.
const email = Session.getActiveUser().getEmail();
Logger.log(email);
```

### getActiveUserLocale() → String

Gets the language setting of the current user as a string—for example, `en` for English.

**Return:** `String` — a string that represents the user's language setting

**Code Sample:**
```javascript
// Log the language setting of the person running the script.
Logger.log(Session.getActiveUserLocale());
```

### getEffectiveUser() → User

Gets information about the user under whose authority the script is running. If the script is a web app set to "execute as me" (the developer), this returns the developer's user account, regardless of who is using the web app. If the script is an installable trigger set to run as the user who installed the trigger, this returns the account of the person who installed the trigger. In most other scenarios, this returns the same account as `getActiveUser()`.

**Return:** `User` — the user under whose authority the script is running

**Authorization:** Scripts that use this method require authorization with one or more of the following scopes: `https://www.googleapis.com/auth/userinfo.email`

**Code Sample:**
```javascript
// Log the email address of the user under whose authority the script is running.
const email = Session.getEffectiveUser().getEmail();
Logger.log(email);
```

### getScriptTimeZone() → String

Gets the time zone of the script. New scripts default to the owner's time zone, but the script's time zone can be changed by clicking File > Project properties in the script editor. This can be an "ordinary" time zone like `America/New_York`, or an offset like `GMT+4:00`.

Note: Spreadsheets have a separate time zone, which can be changed by clicking File > Spreadsheet settings in Google Sheets. Spreadsheet time zones that differ from the script time zone are a frequent source of scripting bugs.

**Return:** `String` — the time zone of the script

**Code Sample:**
```javascript
// Log the time zone of the script.
const timeZone = Session.getScriptTimeZone();
Logger.log(timeZone);
```

### getTemporaryActiveUserKey() → String

Gets a temporary key that is unique to the active user but does not reveal the user identity. The temporary key rotates every 30 days and is unique to the script; the same user will have a different key for two different scripts.

**Return:** `String` — the temporary active user key

**Code Sample:**
```javascript
// Log the temporary key of the person running the script.
Logger.log(Session.getTemporaryActiveUserKey());
```

## Deprecated Methods

### getTimeZone() → String

Deprecated. Use `getScriptTimeZone()` instead.

### getUser() → User

Deprecated. Use `getActiveUser()` instead.
