# PageProtection

Deprecated.

Deprecated. For spreadsheets created in the newer version of Google Sheets, use the more powerful Protection class instead. Although this class is deprecated, it remains available
    for compatibility with the older version of Sheets.

Access and modify protected sheets in the older version of Google Sheets.

## Deprecated Methods

### `addUser(email)`

Deprecated. This function is deprecated and should not be used in new scripts.

Adds a user to the list of users who can edit the sheet, if it is protected.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| email | String | The email of the user to add. |

```javascript
// Add the "user@example.com" user to the list of users who can edit this sheet
const sheet = SpreadsheetApp.getActiveSheet();
const permissions = sheet.getSheetProtection();
permissions.addUser('user@example.com');
permissions.setProtected(true);
sheet.setSheetProtection(permissions);
```

### `getUsers()`

Deprecated. This function is deprecated and should not be used in new scripts.

Returns a list of the email addresses of the users who can edit this sheet.

If sheet protection is disabled, the value returned by this call is meaningless.

**Returns:** String[] — An array of email addresses of users who can edit this sheet.

### `isProtected()`

Deprecated. This function is deprecated and should not be used in new scripts.

Indicates whether the sheet has sheet protection enabled or not.

**Returns:** Boolean — Whether the sheet has sheet protection enabled or not.

```javascript
// Determine whether or not sheet protection is enabled
const sheet = SpreadsheetApp.getActiveSheet();
const permissions = sheet.getSheetProtection();
const isProtected = permissions.isProtected();
```

### `removeUser(user)`

Deprecated. This function is deprecated and should not be used in new scripts.

Removes a user from the list of users who can edit the sheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| user | String | The email address of the user to remove. |

```javascript
// Remove the "user@example.com" user to the list of users who can edit this
// sheet
const sheet = SpreadsheetApp.getActiveSheet();
const permissions = sheet.getSheetProtection();
permissions.removeUser('user@example.com');
permissions.setProtected(true);
sheet.setSheetProtection(permissions);
```

### `setProtected(protection)`

Deprecated. This function is deprecated and should not be used in new scripts.

Sets the protection status for the sheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| protection | Boolean | true to enable sheet protection, false to disable sheet
    protection. |

```javascript
// Enables sheet protection for  this sheet
const sheet = SpreadsheetApp.getActiveSheet();
const permissions = sheet.getSheetProtection();
permissions.setProtected(true);
sheet.setSheetProtection(permissions);
```

