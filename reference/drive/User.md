# User

A user associated with a file in Google Drive.

A user associated with a file in Google Drive. Users can be accessed from `File.getEditors()`, `Folder.getViewers()`, and other methods.

```javascript
const file = DriveApp.getFileById('1234567890abcdefghijklmnopqrstuvwxyz');
const editors = file.getEditors();
for (let i = 0; i < editors.length; i++) {
  Logger.log(editors[i].getEmail());
}
```

## Methods

### getDomain()
**Return type:** `String|null`

Gets the domain name associated with the user's account.

### getEmail()
**Return type:** `String|null`

Gets the user's email address. The user's email address is only available if the user has chosen to share the address from the Google+ account settings page, or if the user belongs to the same domain as the user running the script and the domain administrator has allowed all users within the domain to see other users' email addresses.

### getName()
**Return type:** `String|null`

Gets the user's name. This method returns `null` if the user's name is not available.

### getPhotoUrl()
**Return type:** `String|null`

Gets the URL for the user's photo. This method returns `null` if the user's photo is not available.

### getUserLoginId() — Deprecated
**Return type:** `String`

Deprecated. As of June 24, 2013, replaced by `getEmail()`. Gets the user's email address.
