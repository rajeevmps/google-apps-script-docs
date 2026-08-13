# Protection

Access and modify protected ranges and sheets.

Access and modify protected ranges and sheets. A protected range can protect either a static
range of cells or a named range. A protected sheet may include unprotected regions. For
spreadsheets created with the older version of Google Sheets, use the PageProtection class instead.

To retrieve existing protections, use Sheet.getProtections(type) or Spreadsheet.getProtections(type) .

## Methods

### `addEditor(emailAddress)`

Adds the given user to the list of editors for the protected sheet or range. This method does
not automatically give the user permission to edit the spreadsheet itself; to do that in
addition, call Spreadsheet.addEditor(emailAddress) .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| email Address | String | The email address of the user to add. |

**Returns:** Protection — The object representing the protection settings, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Adds an editor to the spreadsheet using an email address.
// TODO(developer): Replace the email address with a valid email.
ss.addEditor('cloudysanfrancisco@gmail.com');

// Gets a sheet by its name and protects it.
const sheet = ss.getSheetByName('Sheet1');
const sampleProtectedSheet = sheet.protect();

// Adds an editor of the protected sheet using an email address.
// TODO(developer): Replace the email address with a valid email.
sampleProtectedSheet.addEditor('cloudysanfrancisco@gmail.com');

// Gets the editors of the protected sheet.
const editors = sampleProtectedSheet.getEditors();

// Logs the editors' email addresses to the console.
for (const editor of editors) {
  console.log(editor.getEmail());
}
```

### `addEditor(user)`

Adds the given user to the list of editors for the protected sheet or range. This method does
not automatically give the user permission to edit the spreadsheet itself; to do that in
addition, call Spreadsheet.addEditor(user) .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| user | User | A representation of the user to add. |

**Returns:** Protection — The object representing the protection settings, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets a sheet by its name.
const sheet = ss.getSheetByName('Sheet1');

// Protects the sheet.
const sampleProtectedSheet = sheet.protect();

// Adds the active user as an editor of the protected sheet.
sampleProtectedSheet.addEditor(Session.getActiveUser());

// Gets the editors of the protected sheet.
const editors = sampleProtectedSheet.getEditors();

// Logs the editors' email addresses to the console.
for (const editor of editors) {
  console.log(editor.getEmail());
}
```

### `addEditors(emailAddresses)`

Adds the given array of users to the list of editors for the protected sheet or range. This
method does not automatically give the users permission to edit the spreadsheet itself; to do
that in addition, call Spreadsheet.addEditors(emailAddresses) .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| email Addresses | String[] | An array of email addresses of the users to add. |

**Returns:** Protection — The object representing the protection settings, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets a sheet by its name.
const sheet = ss.getSheetByName('Sheet1');

// Creates variables for the email addresses to add as editors.
// TODO(developer): Replace the email addresses with valid ones.
const TEST_EMAIL_1 = 'cloudysanfrancisco@gmail.com';
const TEST_EMAIL_2 = 'baklavainthebalkans@gmail.com';

// Protects the sheet.
const sampleProtectedSheet = sheet.protect();

// Adds editors to the protected sheet using the email address variables.
sampleProtectedSheet.addEditors([TEST_EMAIL_1, TEST_EMAIL_2]);

// Gets the editors of the protected sheet.
const editors = sampleProtectedSheet.getEditors();

// Logs the editors' email addresses to the console.
for (const editor of editors) {
  console.log(editor.getEmail());
}
```

### `addTargetAudience(audienceId)`

Adds the specified target audience as an editor of the protected range.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| audience Id | String | The ID of the target audience to add. |

**Returns:** Protection — The object representing the protection settings, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `canDomainEdit()`

Determines whether all users in the domain that owns the spreadsheet have permission to edit
the protected range or sheet. Throws an exception if the user does not have permission to edit
the protected range or sheet.

**Returns:** Boolean — true if all users in the domain that owns the spreadsheet have permission to
    edit the protected range or sheet; false if they don't.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets a sheet by its name.
const sheet = ss.getSheetByName('Sheet1');

// Protects the sheet.
const sampleProtectedSheet = sheet.protect();

// Logs whether domain users have permission to edit the protected sheet to the
// console.
console.log(sampleProtectedSheet.canDomainEdit());
```

### `canEdit()`

Determines whether the user has permission to edit the protected range or sheet. The
spreadsheet owner is always able to edit protected ranges and sheets.

**Returns:** Boolean — true if the user has permission to edit the protected range or sheet; false if not

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Remove all range protections in the spreadsheet that the user has permission
// to edit.
const ss = SpreadsheetApp.getActive();
const protections = ss.getProtections(SpreadsheetApp.ProtectionType.RANGE);
for (let i = 0; i < protections.length; i++) {
  const protection = protections[i];
  if (protection.canEdit()) {
    protection.remove();
  }
}
```

### `getDescription()`

Gets the description of the protected range or sheet. If no description is set, this method
returns an empty string.

**Returns:** String — The description of the protected range or sheet, or an empty string if no description
    is set.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets a sheet by its name.
const sheet = ss.getSheetByName('Sheet1');

// Protects the sheet and sets the description.
const sampleProtectedSheet =
    sheet.protect().setDescription('Sample sheet is protected');

// Gets the description of the protected sheet and logs it to the console.
const sampleProtectedSheetDescription = sampleProtectedSheet.getDescription();
console.log(sampleProtectedSheetDescription);
```

### `getEditors()`

Gets the list of editors for the protected range or sheet. Throws an exception if the user does
not have permission to edit the protected range or sheet.

**Returns:** User[] — an array of users with permission to edit the protected range or sheet

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Protect the active sheet, then remove all other users from the list of
// editors.
const sheet = SpreadsheetApp.getActiveSheet();
const protection = sheet.protect().setDescription('Sample protected sheet');

// Ensure the current user is an editor before removing others. Otherwise, if
// the user's edit permission comes from a group, the script throws an exception
// upon removing the group.
const me = Session.getEffectiveUser();
protection.addEditor(me);
protection.removeEditors(protection.getEditors());
if (protection.canDomainEdit()) {
  protection.setDomainEdit(false);
}
```

### `getProtectionType()`

Gets the type of the protected area, either RANGE or SHEET .

**Returns:** ProtectionType — The type of protected area, either RANGE or SHEET .

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets a sheet by its name.
const sheet = ss.getSheetByName('Sheet1');

// Protects the sheet.
const sampleProtectedSheet = sheet.protect();

// Gets the type of the protected area.
const protectionType = sampleProtectedSheet.getProtectionType();

// Logs 'SHEET'to the console since the type of the protected area is a sheet.
console.log(protectionType.toString());
```

### `getRange()`

Gets the range that is being protected. If the protection applies to the sheet instead of a
range, this method returns a range that spans the entire sheet.

**Returns:** Range — The range that is being protected.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets a sheet by its name.
const sheet = ss.getSheetByName('Sheet1');

// Gets the range 'A1:B10' of Sheet1.
const range = sheet.getRange('A1:B10');

// Makes cells A1:B10 a protected range.
const sampleProtectedRange = range.protect();

// Gets the protected ranges on the sheet.
const protections = sheet.getProtections(SpreadsheetApp.ProtectionType.RANGE);

// Logs the A1 notation of the first protected range on the sheet.
console.log(protections[0].getRange().getA1Notation());
```

### `getRangeName()`

Gets the name of the protected range if it is associated with a named range. Returns null if the protection is not associated with a named range. Note that scripts must explicitly
call setRangeName(rangeName) to associate a protected range with a named range; calling Range.protect() to create a protection from a Range that happens to be a
named range, without calling setRangeName(rangeName) , is not sufficient to associate
them. However, creating a protected range from a named range in the Google Sheets UI associates
them automatically.

**Returns:** String|null — the name of the protected named range, or null if the protected range is not
    associated with a named range

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Protect a named range in a spreadsheet and log the name of the protected
// range.
const ss = SpreadsheetApp.getActive();
const range = ss.getRange('A1:B10');
const protection = range.protect();
ss.setNamedRange('Test', range);  // Create a named range.
protection.setRangeName(
    'Test');  // Associate the protection with the named range.
Logger.log(
    protection.getRangeName());  // Verify the name of the protected range.
```

### `getTargetAudiences()`

Returns the IDs of the target audiences that can edit the protected range.

**Returns:** TargetAudience[] — An array of the IDs of target audiences.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getUnprotectedRanges()`

Gets an array of unprotected ranges within a protected sheet. If the Protection object
corresponds to a protected range instead of a protected sheet, this method returns an empty
array. To change the unprotected ranges, use setUnprotectedRanges(ranges) to set a
new array of ranges; to re-protect the entire sheet, set an empty array.

**Returns:** Range[] — an array of unprotected ranges within a protected sheet

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Unprotect cells E2:F5 in addition to any other unprotected ranges in the
// protected sheet.
const sheet = SpreadsheetApp.getActiveSheet();
const protection = sheet.protect();
const unprotected = protection.getUnprotectedRanges();
unprotected.push(sheet.getRange('E2:F5'));
protection.setUnprotectedRanges(unprotected);
```

### `isWarningOnly()`

Determines if the protected area is using "warning based" protection. Warning-based protection
means that every user can edit data in the area, except editing prompts a warning asking the
user to confirm the edit. By default, protected ranges or sheets are not warning-based. To
change to the warning state, use setWarningOnly(warningOnly) .

**Returns:** Boolean — true if the protected range or sheet is only using warning-based protection.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets a sheet by its name.
const sheet = ss.getSheetByName('Sheet1');

// Protects the sheet.
const sampleProtectedSheet = sheet.protect();

// Sets the warning status for the protected sheet as true.
sampleProtectedSheet.setWarningOnly(true);

const protectedSheetWarningStatus = sampleProtectedSheet.isWarningOnly();

// Logs the warning status of the protected sheet to the console.
console.log(protectedSheetWarningStatus);
```

### `remove()`

Unprotects the range or sheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Remove all range protections in the spreadsheet that the user has permission
// to edit.
const ss = SpreadsheetApp.getActive();
const protections = ss.getProtections(SpreadsheetApp.ProtectionType.RANGE);
for (let i = 0; i < protections.length; i++) {
  const protection = protections[i];
  if (protection.canEdit()) {
    protection.remove();
  }
}
```

```javascript
// Remove sheet protection from the active sheet, if the user has permission to
// edit it.
const sheet = SpreadsheetApp.getActiveSheet();
const protection = sheet.getProtections(SpreadsheetApp.ProtectionType.SHEET)[0];
if (protection?.canEdit()) {
  protection.remove();
}
```

### `removeEditor(emailAddress)`

Removes the given user from the list of editors for the protected sheet or range. Note that if
the user is a member of a Google Group that has edit permission, or if all users in the domain
have edit permission, the user are still be able to edit the protected area. Neither the owner
of the spreadsheet nor the current user can be removed.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| email Address | String | The email address of the user to remove. |

**Returns:** Protection — The object representing the protection settings, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets a sheet by its name.
const sheet = ss.getSheetByName('Sheet1');

// Creates a variable for an email address.
// TODO(developer): Replace the email address with a valid one.
const TEST_EMAIL = 'baklavainthebalkans@gmail.com';

// Protects the sheet.
const sampleProtectedSheet = sheet.protect();

// Adds an editor to the protected sheet using the email address variable.
sampleProtectedSheet.addEditor(TEST_EMAIL);

// Removes the editor from the protected sheet using the email address variable.
sampleProtectedSheet.removeEditor(TEST_EMAIL);

// Gets the editors of the protected sheet.
const editors = sampleProtectedSheet.getEditors();

// Logs the editors' email addresses to the console.
for (const editor of editors) {
  console.log(editor.getEmail());
}
```

### `removeEditor(user)`

Removes the given user from the list of editors for the protected sheet or range. Note that if
the user is a member of a Google Group that has edit permission, or if all users in the domain
have edit permission, the user is still be able to edit the protected area as well. Neither the
owner of the spreadsheet nor the current user can be removed.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| user | User | A representation of the user to remove. |

**Returns:** Protection — the object representing the protection settings, for chaining

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets a sheet by its name.
const sheet = ss.getSheetByName('Sheet1');

// Protects the sheet.
const sampleProtectedSheet = sheet.protect();

// Removes the active user from the editors of the protected sheet.
sampleProtectedSheet.removeEditor(Session.getActiveUser());

// Gets the editors of the protected sheet.
const editors = sampleProtectedSheet.getEditors();

// Logs the editors' email addresses to the console.
for (const editor of editors) {
  console.log(editor.getEmail());
}
```

### `removeEditors(emailAddresses)`

Removes the given array of users from the list of editors for the protected sheet or range.
Note that if any of the users are members of a Google Group that has edit permission, or if all
users in the domain have edit permission, those users are still be able to edit the protected
area. Neither the owner of the spreadsheet nor the current user can be removed.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| email Addresses | String[] | An array of email addresses of the users to remove. |

**Returns:** Protection — the object representing the protection settings, for chaining

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Protect the active sheet, then remove all other users from the list of
// editors.
const sheet = SpreadsheetApp.getActiveSheet();
const protection = sheet.protect().setDescription('Sample protected sheet');

// Ensure the current user is an editor before removing others. Otherwise, if
// the user's edit permission comes from a group, the script throws an exception
// upon removing the group.
const me = Session.getEffectiveUser();
protection.addEditor(me);
protection.removeEditors(protection.getEditors());
if (protection.canDomainEdit()) {
  protection.setDomainEdit(false);
}
```

### `removeTargetAudience(audienceId)`

Removes the specified target audience as an editor of the protected range.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| audience Id | String | The ID of the target audience to remove. |

**Returns:** Protection — The object representing the protection settings, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setDescription(description)`

Sets the description of the protected range or sheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| description | String | The description of the protected range or sheet. |

**Returns:** Protection — The object representing the protection settings, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets the sheet 'Sheet1' by its name.
const sheet = ss.getSheetByName('Sheet1');

// Protects the sheet.
const sampleProtectedSheet = sheet.protect();

// Sets the sheet description to 'Sheet1 is protected.'
sampleProtectedSheet.setDescription('Sheet1 is protected');

// Gets the description of the protected sheet.
const sampleProtectedSheetDescription = sampleProtectedSheet.getDescription();

// Logs the description of the protected sheet to the console.
console.log(sampleProtectedSheetDescription);
```

### `setDomainEdit(editable)`

Sets whether all users in the domain that owns the spreadsheet have permission to edit the
protected range or sheet. Note that any users who have explicit edit permission are able to
edit the protected area regardless of this setting. Throws an exception if the spreadsheet does
not belong to a Google Workspace domain (that is, if it is owned by a gmail.com account).

**Parameters:**

| Name | Type | Description |
|---|---|---|
| editable | Boolean | true if all users in the domain that owns the spreadsheet should have
    permission to edit the protected range or sheet; false if not. |

**Returns:** Protection — the object representing the protection settings, for chaining

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setNamedRange(namedRange)`

Associates the protected range with an existing named range. If the named range covers a
different area from the current protected range, this method moves the protection to cover the
the named range instead. The named range must be on the same sheet as the current protected
range. Note that scripts must explicitly call this method to associate a protected range with a
named range; calling Range.protect() to create a protection from a Range that happens to be a named range, without calling setRangeName(rangeName) , is not
sufficient to associate them. However, creating a protected range from a named range in the
Google Sheets UI associates them automatically.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| named Range | Named Range | The existing named range to associate with the protected range. |

**Returns:** Protection — The object representing the protection settings, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Protects cells A1:D10 on Sheet1.
const sheet = ss.getSheetByName('Sheet1');
const protectedRange = sheet.getRange('A1:D10').protect();

// Logs the current protected range, A1:D10.
console.log(protectedRange.getRange().getA1Notation());

// Creates a named range for cells E1:J10 called 'NewRange.'
const newRange = sheet.getRange('E1:J10');
ss.setNamedRange('NewRange', newRange);
const namedRange = ss.getNamedRanges()[0];

// Updates the protected range to the named range, 'NewRange.'
// This updates the protected range on Sheet1 from A1:D10 to E1:J10.
protectedRange.setNamedRange(namedRange);

// Logs the updated protected range to the console.
console.log(protectedRange.getRange().getA1Notation());
```

### `setRange(range)`

Adjusts the range that is being protected. If the given range covers a different area from the
current protected range, this method moves the protection to cover the new range instead.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| range | Range | The new range to protect from edits. |

**Returns:** Protection — The object representing the protection settings, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Protects cells A1:D10 on Sheet1 of the spreadsheet.
const sheet = ss.getSheetByName('Sheet1');
const protectedRange = sheet.getRange('A1:D10').protect();

// Logs the original protected range, A1:D10, to the console.
console.log(protectedRange.getRange().getA1Notation());

// Gets the range E1:J10.
const newRange = sheet.getRange('E1:J10');

// Updates the protected range to E1:J10.
protectedRange.setRange(newRange);

// Logs the updated protected range to the console.
console.log(protectedRange.getRange().getA1Notation());
```

### `setRangeName(rangeName)`

Associates the protected range with an existing named range. If the named range covers a
different area from the current protected range, this method moves the protection to cover the
the named range instead. The named range must be on the same sheet as the current protected
range. Note that scripts must explicitly call this method to associate a protected range with a
named range; calling Range.protect() to create a protection from a Range that happens to be a named range, without calling setRangeName(rangeName) , is not
sufficient to associate them. However, creating a protected range from a named range in the
Google Sheets UI associates them automatically.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| range Name | String | The name of the named range to be protected. |

**Returns:** Protection — the object representing the protection settings, for chaining

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Protect a named range in a spreadsheet and log the name of the protected
// range.
const ss = SpreadsheetApp.getActive();
const range = ss.getRange('A1:B10');
const protection = range.protect();
ss.setNamedRange('Test', range);  // Create a named range.
protection.setRangeName(
    'Test');  // Associate the protection with the named range.
Logger.log(
    protection.getRangeName());  // Verify the name of the protected range.
```

### `setUnprotectedRanges(ranges)`

Unprotects the given array of ranges within a protected sheet. Throws an exception if the Protection object corresponds to a protected range instead of a protected sheet or if
any of the ranges are not on the protected sheet. To change the unprotected ranges, set a new
array of ranges; to re-protect the entire sheet, set an empty array.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| ranges | Range[] | The array of ranges to leave unprotected within a protected sheet. |

**Returns:** Protection — the object representing the protection settings, for chaining

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Protect the active sheet except B2:C5, then remove all other users from the
// list of editors.
const sheet = SpreadsheetApp.getActiveSheet();
const protection = sheet.protect().setDescription('Sample protected sheet');
const unprotected = sheet.getRange('B2:C5');
protection.setUnprotectedRanges([unprotected]);

// Ensure the current user is an editor before removing others. Otherwise, if
// the user's edit permission comes from a group, the script throws an exception
// upon removing the group.
const me = Session.getEffectiveUser();
protection.addEditor(me);
protection.removeEditors(protection.getEditors());
if (protection.canDomainEdit()) {
  protection.setDomainEdit(false);
}
```

### `setWarningOnly(warningOnly)`

Sets whether or not this protected range is using "warning based" protection. Warning-based
protection means that every user can edit data in the area, except editing prompts a warning
asking the user to confirm the edit. By default, protected ranges or sheets are not
warning-based. To check warning state, use isWarningOnly() .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| warning Only | Boolean |  |

**Returns:** Protection — The object representing the protection settings, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets the sheet 'Sheet1' by its name.
const sheet = ss.getSheetByName('Sheet1');

// Protects the sheet and sets the protection to warning-based.
const sampleProtectedSheet = sheet.protect().setWarningOnly(true);

// Logs whether the protected sheet is warning-based to the console.
console.log(sampleProtectedSheet.isWarningOnly());
```

