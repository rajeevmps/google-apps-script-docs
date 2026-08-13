# Spreadsheet

Access and modify Google Sheets files.

Access and modify Google Sheets files. Common operations are adding new sheets and adding
collaborators.

## Methods

### `addDeveloperMetadata(key)`

Adds developer metadata with the specified key to the top-level spreadsheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| key | String | The key for the new developer metadata. |

**Returns:** Spreadsheet — This spreadsheet, for chaining.

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

// Adds the key 'NAME' in the developer metadata for the spreadsheet.
ss.addDeveloperMetadata('NAME');

// Gets the first developer metadata object and logs its key.
const developerMetaData = ss.getDeveloperMetadata()[0];
console.log(developerMetaData.getKey());
```

### `addDeveloperMetadata(key, visibility)`

Adds developer metadata with the specified key and visibility to the spreadsheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| key | String | The key for the new developer metadata. |
| visibility | Developer Metadata Visibility | The visibility of the new developer metadata. |

**Returns:** Spreadsheet — This spreadsheet, for chaining.

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

// Adds the key 'NAME' in the developer metadata for the spreadsheet and sets
// the visibility to the developer project that created the metadata.
ss.addDeveloperMetadata(
    'NAME',
    SpreadsheetApp.DeveloperMetadataVisibility.PROJECT,
);

// Gets the first developer metadata object and logs its key and visibility
// setting.
const developerMetaData = ss.getDeveloperMetadata()[0];
console.log(developerMetaData.getKey());
console.log(`Key: ${developerMetaData.getKey()},
.             Visibility: ${developerMetaData.getVisibility()}`);
```

### `addDeveloperMetadata(key, value)`

Adds developer metadata with the specified key and value to the spreadsheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| key | String | The key for the new developer metadata. |
| value | String | The value for the new developer metadata. |

**Returns:** Spreadsheet — This spreadsheet, for chaining.

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

// Adds the key 'NAME' and sets the value to 'GOOGLE' in the developer metadata
// for the spreadsheet.
ss.addDeveloperMetadata('NAME', 'GOOGLE');

// Gets the first developer metadata object and logs its key and value.
const developerMetaData = ss.getDeveloperMetadata()[0];
console.log(developerMetaData.getKey());
console.log(
    `Key: ${developerMetaData.getKey()}, Value: ${
        developerMetaData.getValue()}`,
);
```

### `addDeveloperMetadata(key, value, visibility)`

Adds developer metadata with the specified key, value, and visibility to the spreadsheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| key | String | The key for the new developer metadata. |
| value | String | The value for the new developer metadata. |
| visibility | Developer Metadata Visibility | The visibility of the new developer metadata. |

**Returns:** Spreadsheet — This spreadsheet, for chaining.

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

// Adds the key 'NAME', sets the value to 'GOOGLE', and sets the visibility
// to any developer project with document access.
ss.addDeveloperMetadata(
    'NAME',
    'GOOGLE',
    SpreadsheetApp.DeveloperMetadataVisibility.DOCUMENT,
);

// Gets the first developer metadata object and logs its key, value, and
// visibility setting.
const developerMetaData = ss.getDeveloperMetadata()[0];
console.log(`Key: ${developerMetaData.getKey()},
             Value: ${developerMetaData.getValue()},
             Visibility: ${developerMetaData.getVisibility()}`);
```

### `addEditor(emailAddress)`

Adds the given user to the list of editors for the Spreadsheet . If the user was already
on the list of viewers, this method promotes the user out of the list of viewers.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| email Address | String | The email address of the user to add. |

**Returns:** Spreadsheet — This Spreadsheet , for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `addEditor(user)`

Adds the given user to the list of editors for the Spreadsheet . If the user was already
on the list of viewers, this method promotes the user out of the list of viewers.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| user | User | A representation of the user to add. |

**Returns:** Spreadsheet — This Spreadsheet , for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `addEditors(emailAddresses)`

Adds the given array of users to the list of editors for the Spreadsheet . If any of the
users were already on the list of viewers, this method promotes them out of the list of
viewers.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| email Addresses | String[] | An array of email addresses of the users to add. |

**Returns:** Spreadsheet — This Spreadsheet , for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `addMenu(name, subMenus)`

Creates a new menu in the Spreadsheet UI.

Each menu entry runs a user-defined function. Usually, you want to call it from the onOpen() function so that the menu is automatically created when the spreadsheet is loaded.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| name | String | The name of the menu to be created. |
| sub Menus | Object[] | An array of JavaScript maps with name and function Name parameters. You can use functions from included libraries, such as Library.libFunction1 . |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// The onOpen function is executed automatically every time a Spreadsheet is
// loaded
function onOpen() {
  const ss = SpreadsheetApp.getActiveSpreadsheet();
  const menuEntries = [];
  // When the user clicks on "addMenuExample" then "Menu Entry 1", the function
  // function1 is executed.
  menuEntries.push({name: 'Menu Entry 1', functionName: 'function1'});
  menuEntries.push(null);  // line separator
  menuEntries.push({name: 'Menu Entry 2', functionName: 'function2'});

  ss.addMenu('addMenuExample', menuEntries);
}
```

### `addViewer(emailAddress)`

Adds the given user to the list of viewers for the Spreadsheet . If the user was already
on the list of editors, this method has no effect.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| email Address | String | The email address of the user to add. |

**Returns:** Spreadsheet — This Spreadsheet , for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `addViewer(user)`

Adds the given user to the list of viewers for the Spreadsheet . If the user was already
on the list of editors, this method has no effect.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| user | User | A representation of the user to add. |

**Returns:** Spreadsheet — This Spreadsheet , for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `addViewers(emailAddresses)`

Adds the given array of users to the list of viewers for the Spreadsheet . If any of the
users were already on the list of editors, this method has no effect for them.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| email Addresses | String[] | An array of email addresses of the users to add. |

**Returns:** Spreadsheet — This Spreadsheet , for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `appendRow(rowContents)`

Appends a row to the bottom of the current data region in the sheet. If a cell's content begins
with = , it's interpreted as a formula.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| row Contents | Object[] | An array of values to insert after the last row in the sheet. |

**Returns:** Sheet — The sheet, useful for method chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// Appends a new row with 3 columns to the bottom of the current
// data region in the sheet containing the values in the array.
sheet.appendRow(['a man', 'a plan', 'panama']);
```

### `autoResizeColumn(columnPosition)`

Sets the width of the given column to fit its contents.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| column Position | Integer | The position of the given column to resize. |

**Returns:** Sheet — The sheet, useful for method chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

sheet.getRange('a1').setValue(
    'Whenever it is a damp, drizzly November in my soul...');

// Sets the first column to a width which fits the text
sheet.autoResizeColumn(1);
```

### `copy(name)`

Copies the spreadsheet and returns the new one.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| name | String | The name of the copy. |

**Returns:** Spreadsheet — This spreadsheet, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// This code makes a copy of the current spreadsheet and names it appropriately
const ss = SpreadsheetApp.getActiveSpreadsheet();
ss.copy(`Copy of ${ss.getName()}`);
```

### `createDeveloperMetadataFinder()`

Returns a DeveloperMetadataFinder for finding developer metadata within the scope of
this spreadsheet. By default this considers all metadata associated with the spreadsheet,
sheets, rows, and columns.

**Returns:** DeveloperMetadataFinder — A developer metadata finder to search for metadata in the scope of this spreadsheet.

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Adds developer metadata to the spreadsheet.
ss.addDeveloperMetadata('NAME', 'CHARLIE');
ss.addDeveloperMetadata('COMPANY', 'EXAMPLE ORGANIZATION');
ss.addDeveloperMetadata('TECHNOLOGY', 'JAVASCRIPT');

// Creates a developer metadata finder.
const developerMetadataFinder = ss.createDeveloperMetadataFinder();

// Finds the developer metadata objects with 'COMPANY' as the key.
const googleMetadataFromSpreadsheet =
    developerMetadataFinder.withKey('COMPANY').find();

// Gets the first result of developer metadata that has the key 'COMPANY' and
// logs its value.
console.log(googleMetadataFromSpreadsheet[0].getValue());
```

### `createTextFinder(findText)`

Creates a text finder for the spreadsheet, which can be used to find and replace text within
the spreadsheet. The search starts from the first sheet of the spreadsheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| find Text | String | The text to search for. |

**Returns:** TextFinder — The TextFinder for the spreadsheet.

```javascript
const spreadsheet = SpreadsheetApp.getActiveSpreadsheet();

// Creates  a text finder.
const textFinder = spreadsheet.createTextFinder('dog');

// Returns the first occurrence of 'dog' in the spreadsheet.
const firstOccurrence = textFinder.findNext();

// Replaces the last found occurrence of 'dog' with 'cat' and returns the number
// of occurrences replaced.
const numOccurrencesReplaced = textFinder.replaceWith('cat');
```

### `deleteActiveSheet()`

Deletes the currently active sheet.

**Returns:** Sheet — The new active sheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// The code below deletes the currently active sheet and stores the new active
// sheet in a variable
const newSheet = SpreadsheetApp.getActiveSpreadsheet().deleteActiveSheet();
```

### `deleteColumn(columnPosition)`

Deletes the column at the given column position.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| column Position | Integer | The position of the column, starting at 1 for the first column. |

**Returns:** Sheet — The sheet, useful for method chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];
// Columns start at "1" - this deletes the first column
sheet.deleteColumn(1);
```

### `deleteColumns(columnPosition, howMany)`

Deletes a number of columns starting at the given column position.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| column Position | Integer | The position of the first column to delete. |
| how Many | Integer | The number of columns to delete. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];
// Columns start at "1" - this deletes the first two columns
sheet.deleteColumns(1, 2);
```

### `deleteRow(rowPosition)`

Deletes the row at the given row position.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| row Position | Integer | The position of the row, starting at 1 for the first row. |

**Returns:** Sheet — The sheet, useful for method chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];
// Rows start at "1" - this deletes the first row
sheet.deleteRow(1);
```

### `deleteRows(rowPosition, howMany)`

Deletes a number of rows starting at the given row position.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| row Position | Integer | The position of the first row to delete. |
| how Many | Integer | The number of rows to delete. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];
// Rows start at "1" - this deletes the first two rows
sheet.deleteRows(1, 2);
```

### `deleteSheet(sheet)`

Deletes the specified sheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| sheet | Sheet | The sheet to delete. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// The code below deletes the specified sheet.
const ss = SpreadsheetApp.getActive();
const sheet = ss.getSheetByName('My Sheet');
ss.deleteSheet(sheet);
```

### `duplicateActiveSheet()`

Duplicates the active sheet and makes it the active sheet.

**Returns:** Sheet — The new sheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// The code below makes a duplicate of the active sheet
SpreadsheetApp.getActiveSpreadsheet().duplicateActiveSheet();
```

### `getActiveCell()`

Returns the active cell in this sheet.

Note: It's preferable to use getCurrentCell() , which returns the current
highlighted cell.

**Returns:** Range — The current active cell.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];
// Returns the active cell
const cell = sheet.getActiveCell();
```

### `getActiveRange()`

Returns the selected range in the active sheet, or null if there is no active range. If
multiple ranges are selected this method returns only the last selected range.

The term "active range" refers to the range that a user has selected in the active sheet,
but in a custom function it refers to the cell being actively recalculated.

**Returns:** Range — The active range.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
const activeRange = sheet.getActiveRange();
```

### `getActiveRangeList()`

Returns the list of active ranges in the active sheet or null if there are no active
ranges.

If there is a single range selected, this behaves as a getActiveRange() call.

**Returns:** RangeList |null — The list of active ranges.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
// Returns the list of active ranges.
const activeRangeList = sheet.getActiveRangeList();
```

### `getActiveSheet()`

Gets the active sheet in a spreadsheet.

The active sheet in a spreadsheet is the sheet that is being displayed in the spreadsheet
UI.

**Returns:** Sheet — The active sheet in the spreadsheet.

```javascript
const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
```

### `getAs(contentType)`

Return the data inside this object as a blob converted to the specified content type. This
method adds the appropriate extension to the filename—for example, "myfile.pdf". However, it
assumes that the part of the filename that follows the last period (if any) is an existing
extension that should be replaced. Consequently, "ShoppingList.12.25.2014" becomes
"ShoppingList.12.25.pdf".

To view the daily quotas for conversions, see Quotas for Google
Services . Newly created Google Workspace domains might be temporarily subject to stricter
quotas.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| content Type | String | The MIME type to convert to. For most blobs, 'application/pdf' is
    the only valid option. For images in BMP, GIF, JPEG, or PNG format, any of 'image/bmp' , 'image/gif' , 'image/jpeg' , or 'image/png' are also
    valid. For a Google Docs document, 'text/markdown' is also valid. |

**Returns:** Blob — The data as a blob.

### `getBandings()`

Returns all the bandings in this spreadsheet.

**Returns:** Banding[] — The bandings in this spreadsheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets spreadsheet, you can use
// SpreadsheetApp.getActiveSpreadsheet() instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets an array of the bandings in the spreadsheet.
const bandings = ss.getBandings();

// Logs the range of the first banding in the spreadsheet to the console.
console.log(bandings[0].getRange().getA1Notation());
```

### `getBlob()`

Return the data inside this object as a blob.

**Returns:** Blob — The data as a blob.

### `getColumnWidth(columnPosition)`

Gets the width in pixels of the given column.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| column Position | Integer | The position of the column to examine. |

**Returns:** Integer — Column width in pixels.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// Columns start at 1
Logger.log(sheet.getColumnWidth(1));
```

### `getCurrentCell()`

Returns the current cell in the active sheet or null if there is no current cell. The
current cell is the cell that has focus in the Google Sheets UI, and is highlighted by a dark
border. There is never more than one current cell. When a user selects one or more cell ranges,
one of the cells in the selection is the current cell.

**Returns:** Range |null — The current cell.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
// Returns the current highlighted cell in the one of the active ranges.
const currentCell = sheet.getCurrentCell();
```

### `getDataRange()`

Returns a Range corresponding to the dimensions in which data is present.

This is functionally equivalent to creating a Range bounded by A1 and
(Sheet.getLastColumn(), Sheet.getLastRow()).

**Returns:** Range — A range consisting of all the data in the spreadsheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// This represents ALL the data
const range = sheet.getDataRange();
const values = range.getValues();

// This logs the spreadsheet in CSV format with a trailing comma
for (let i = 0; i < values.length; i++) {
  let row = '';
  for (let j = 0; j < values[i].length; j++) {
    if (values[i][j]) {
      row = row + values[i][j];
    }
    row = `${row},`;
  }
  Logger.log(row);
}
```

### `getDataSourceFormulas()`

Gets all the data source formulas.

**Returns:** DataSourceFormula[] — A list of data source formulas.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet by its ID. If you created your script from within a
// Google Sheets file, use SpreadsheetApp.getActiveSpreadsheet().
// TODO(developer): Replace the ID with your own.
const ss = SpreadsheetApp.openById('abc123456');

// Gets Sheet1 by its name.
const sheet = ss.getSheetByName('Sheet1');

// Gets an array of the data source formulas on Sheet1.
// To get an array of data source formulas for the entire spreadsheet,
// replace 'sheet' with 'ss'.
const dataSourceFormulas = sheet.getDataSourceFormulas();

// Logs the first data source formula in the array.
console.log(dataSourceFormulas[0].getFormula());
```

### `getDataSourcePivotTables()`

Gets all the data source pivot tables.

**Returns:** DataSourcePivotTable[] — A list of data source pivot tables.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its ID. If you created your script from a
// Google Sheets file, use SpreadsheetApp.getActiveSpreadsheet().
// TODO(developer): Replace the ID with your own.
const ss = SpreadsheetApp.openById('abc123456');

// Gets Sheet1 by its name.
const sheet = ss.getSheetByName('Sheet1');

// Gets an array of the data source pivot tables on Sheet1.
// To get an array of data source pivot tables for the entire
// spreadsheet, replace 'sheet' with 'ss'.
const dataSourcePivotTables = sheet.getDataSourcePivotTables();

// Logs the last time that the first pivot table in the array was refreshed.
console.log(dataSourcePivotTables[0].getStatus().getLastRefreshedTime());
```

### `getDataSourceRefreshSchedules()`

Gets the refresh schedules of this spreadsheet.

**Returns:** DataSourceRefreshSchedule[] — The refresh schedules of this spreadsheet.

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

// Activates BigQuery operations for the connected spreadsheet.
SpreadsheetApp.enableBigQueryExecution();

// Gets the frequency type of the first referesh schedule in the array.
const frequencyType = ss.getDataSourceRefreshSchedules()[0]
                          .getFrequency()
                          .getFrequencyType()
                          .toString();

// Logs the frequency type to the console.
console.log(frequencyType);
```

### `getDataSourceSheets()`

Returns all the data source sheets in the spreadsheet.

**Returns:** DataSourceSheet[] — An array of all the data source sheets.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Turns data execution on for BigQuery data sources.
SpreadsheetApp.enableBigQueryExecution();

// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets spreadsheet, you can use
// SpreadsheetApp.getActiveSpreadsheet() instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets the first data source sheet in the spreadsheet.
const dataSource = ss.getDataSourceSheets()[0];

// Gets the name of the data source sheet.
console.log(dataSource.asSheet().getName());
```

### `getDataSourceTables()`

Gets all the data source tables.

**Returns:** DataSourceTable[] — A list of data source tables.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its ID. If you created your script from a
// Google Sheets file, use SpreadsheetApp.getActiveSpreadsheet().
// TODO(developer): Replace the ID with your own.
const ss = SpreadsheetApp.openById('abc123456');

// Gets Sheet1 by its name.
const sheet = ss.getSheetByName('Sheet1');

// Gets an array of data source tables on Sheet1.
// To get an array of data source tables for the entire spreadsheet,
// replace 'sheet' with 'ss'.
const dataSourceTables = sheet.getDataSourceTables();

// Logs the last completed data execution time on the first data source table.
console.log(dataSourceTables[0].getStatus().getLastExecutionTime());
```

### `getDataSources()`

Returns all the data sources in the spreadsheet.

**Returns:** DataSource[] — An array of all the data sources.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Turns data execution on for BigQuery data sources.
SpreadsheetApp.enableBigQueryExecution();

// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets spreadsheet, you can use
// SpreadsheetApp.getActiveSpreadsheet() instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets the data sources on the spreadsheet.
const dataSources = ss.getDataSources();

// Logs the name of the first column on the first data source.
console.log(dataSources[0].getColumns()[0].getName());
```

### `getDeveloperMetadata()`

Gets the developer metadata associated with the top-level spreadsheet.

**Returns:** DeveloperMetadata[] — The developer metadata associated with this range.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets spreadsheet, you can use
// SpreadsheetApp.getActiveSpreadsheet() instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Adds 'Google' as a key to the spreadsheet metadata.
ss.addDeveloperMetadata('Google');

// Gets the spreadsheet's metadata.
const ssMetadata = ss.getDeveloperMetadata();

// Gets the first set of the spreadsheet's metadata and logs the key to the
// console.
console.log(ssMetadata[0].getKey());
```

### `getEditors()`

Gets the list of editors for this Spreadsheet .

**Returns:** User[] — An array of users with edit permission.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getFormUrl()`

Returns the URL for the form that sends its responses to this spreadsheet, or null if
this spreadsheet has no associated form. If multiple forms send responses to this spreadsheet,
the form URL returned is indeterminate. As an alternative, per sheet form URL associations can
be retrieved through the Sheet.getFormUrl() method. Throws an exception if the user
does not have permission to edit the spreadsheet.

**Returns:** String — The URL for the form that places its responses in this spreadsheet, or null if
    this spreadsheet doesn't have an associated form.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets spreadsheet, you can use
// SpreadsheetApp.getActiveSpreadsheet() instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets the form URL from the spreadsheet.
const formUrl = ss.getFormUrl();

// Logs the form URL to the console.
console.log(formUrl);
```

### `getFrozenColumns()`

Returns the number of frozen columns.

**Returns:** Integer — The number of frozen columns.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

Logger.log('Number of frozen columns: %s', sheet.getFrozenColumns());
```

### `getFrozenRows()`

Returns the number of frozen rows.

**Returns:** Integer — The number of frozen rows.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

Logger.log('Number of frozen rows: %s', sheet.getFrozenRows());
```

### `getId()`

Gets a unique identifier for this spreadsheet. A spreadsheet ID can be extracted from its URL.
For example, the spreadsheet ID in the URL
https://docs.google.com/spreadsheets/d/abc1234567/edit#gid=0 is "abc1234567".

**Returns:** String — The unique ID (or key) for the spreadsheet.

```javascript
// The code below logs the ID for the active spreadsheet.
Logger.log(SpreadsheetApp.getActiveSpreadsheet().getId());
```

### `getImages()`

Returns all over-the-grid images on the sheet.

**Returns:** OverGridImage[] — An array of over-the-grid images.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets spreadsheet, you can use
// SpreadsheetApp.getActiveSpreadsheet() instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets Sheet1 by its name.
const sheet = ss.getSheetByName('Sheet1');

// Gets the over-the-grid images from Sheet1.
// To get the over-the-grid images from the entire spreadsheet, use
// ss.getImages() instead.
const images = sheet.getImages();

// For each image, logs the anchor cell in A1 notation.
for (const image of images) {
  console.log(image.getAnchorCell().getA1Notation());
}
```

### `getIterativeCalculationConvergenceThreshold()`

Returns the threshold value used during iterative calculation. When the results of successive
calculation differ by less than this value, the iterative calculation stops.

**Returns:** Number — The convergence threshold.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets spreadsheet, you can use
// SpreadsheetApp.getActiveSpreadsheet() instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Sets the iterative calculation convergence threshold for the spreadsheet.
ss.setIterativeCalculationConvergenceThreshold(2);

// Logs the threshold to the console.
console.log(ss.getIterativeCalculationConvergenceThreshold());
```

### `getLastColumn()`

Returns the position of the last column that has content.

**Returns:** Integer — The last column of the sheet that contains content.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// This logs the value in the very last cell of this sheet
const lastRow = sheet.getLastRow();
const lastColumn = sheet.getLastColumn();
const lastCell = sheet.getRange(lastRow, lastColumn);
Logger.log(lastCell.getValue());
```

### `getLastRow()`

Returns the position of the last row that has content.

**Returns:** Integer — The last row of the sheet that contains content.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// This logs the value in the very last cell of this sheet
const lastRow = sheet.getLastRow();
const lastColumn = sheet.getLastColumn();
const lastCell = sheet.getRange(lastRow, lastColumn);
Logger.log(lastCell.getValue());
```

### `getMaxIterativeCalculationCycles()`

Returns the maximum number of iterations to use during iterative calculation.

**Returns:** Integer — The maximum number of calculation iterations.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets spreadsheet, you can use
// SpreadsheetApp.getActiveSpreadsheet() instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Sets the max iterative calculation cycles for the spreadsheet.
ss.setMaxIterativeCalculationCycles(10);

// Logs the max iterative calculation cycles to the console.
console.log(ss.getMaxIterativeCalculationCycles());
```

### `getName()`

Gets the name of the document.

**Returns:** String — The name of the spreadsheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
Logger.log(ss.getName());
```

### `getNamedRanges()`

Gets all the named ranges in this spreadsheet.

**Returns:** NamedRange[] — An array of all the named ranges in the spreadsheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// The code below logs the name of the first named range.
const namedRanges = SpreadsheetApp.getActiveSpreadsheet().getNamedRanges();
for (let i = 0; i < namedRanges.length; i++) {
  Logger.log(namedRanges[i].getName());
}
```

### `getNumSheets()`

Returns the number of sheets in this spreadsheet.

**Returns:** Integer — The number of sheets in the spreadsheet.

```javascript
// The code below logs the number of sheets in the active spreadsheet.
Logger.log(SpreadsheetApp.getActiveSpreadsheet().getNumSheets());
```

### `getOwner()`

Returns the owner of the document, or null for a document in a shared drive.

**Returns:** User — The owner of the document, or null if the document is in a shared drive.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const owner = ss.getOwner();
Logger.log(owner.getEmail());
```

### `getPredefinedSpreadsheetThemes()`

Returns the list of predefined themes.

**Returns:** SpreadsheetTheme[] — List of predefined themes.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// The code below returns the list of predefined themes.
const predefinedThemesList =
    SpreadsheetApp.getActiveSpreadsheet().getPredefinedSpreadsheetThemes();
```

### `getProtections(type)`

Gets an array of objects representing all protected ranges or sheets in the spreadsheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| type | Protection Type | The type of protected area, either Spreadsheet App.ProtectionType.RANGE or Spreadsheet App.ProtectionType.SHEET . |

**Returns:** Protection[] — An array of objects representing all protected ranges or sheets in the spreadsheet.

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
// Remove all sheet protections in the spreadsheet that the user has permission
// to edit.
const ss = SpreadsheetApp.getActive();
const protections = ss.getProtections(SpreadsheetApp.ProtectionType.SHEET);
for (let i = 0; i < protections.length; i++) {
  const protection = protections[i];
  if (protection.canEdit()) {
    protection.remove();
  }
}
```

### `getRange(a1Notation)`

Returns the range as specified in A1 notation or R1C1 notation.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| a1Notation | String | The range to return, as specified in A1 notation or R1C1 notation. |

**Returns:** Range — The range at the location designated.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Get a range A1:D4 on sheet titled "Invoices"
const ss = SpreadsheetApp.getActiveSpreadsheet();
const range = ss.getRange('Invoices!A1:D4');

// Get cell A1 on the first sheet
const sheet = ss.getSheets()[0];
const cell = sheet.getRange('A1');
```

### `getRangeByName(name)`

Returns a named range, or null if no range with the given name is found. If multiple
sheets of the spreadsheet use the same range name, specify the sheet name without additional
quotation marks — for example, getRangeByName('TaxRates') or getRangeByName('Sheet Name!TaxRates') , but not getRangeByName('"Sheet
Name"!TaxRates') .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| name | String | The name of the range to get. |

**Returns:** Range — The range of cells with the given name.

```javascript
// Log the number of columns for the range named 'TaxRates' in the active
// spreadsheet.
const range = SpreadsheetApp.getActiveSpreadsheet().getRangeByName('TaxRates');
if (range != null) {
  Logger.log(range.getNumColumns());
}
```

### `getRangeList(a1Notations)`

Returns the RangeList collection representing the ranges in the same sheet specified
by a non-empty list of A1 notations or R1C1 notations.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| a1Notations | String[] | The list of ranges to return, as specified in A1 notation or R1C1 notation. |

**Returns:** RangeList — The range list at the location designated.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Get a list of ranges A1:D4, F1:H4.
const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
const rangeList = sheet.getRangeList(['A1:D4', 'F1:H4']);
```

### `getRecalculationInterval()`

Returns the calculation interval for this spreadsheet.

**Returns:** RecalculationInterval — The calculation interval for this spreadsheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets spreadsheet, you can use
// SpreadsheetApp.getActiveSpreadsheet() instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Logs the calculation interval for the spreadsheet to the console.
console.log(ss.getRecalculationInterval().toString());
```

### `getRowHeight(rowPosition)`

Gets the height in pixels of the given row.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| row Position | Integer | The position of the row to examine. |

**Returns:** Integer — Row height in pixels.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// Rows start at 1
Logger.log(sheet.getRowHeight(1));
```

### `getSelection()`

Returns the current Selection in the spreadsheet.

**Returns:** Selection — The current selection.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const selection = SpreadsheetApp.getActiveSpreadsheet().getSelection();
const currentCell = selection.getCurrentCell();
```

### `getSheetById(id)`

Gets the sheet with the given ID. Use Sheet.getSheetId() .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| id | Integer | The ID of the sheet to get. |

**Returns:** Sheet |null — The sheet with the given ID or null if no sheet is found.

```javascript
const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetById(12345);
```

### `getSheetByName(name)`

Returns a sheet with the given name.

If multiple sheets have the same name, the leftmost one is returned. Returns null if
there is no sheet with the given name.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| name | String | The name of the sheet to get. |

**Returns:** Sheet |null — The sheet with the given name, or null if no sheet is found.

```javascript
// The code below logs the index of a sheet named "Expenses"
const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Expenses');
if (sheet != null) {
  Logger.log(sheet.getIndex());
}
```

### `getSheetId()`

Returns the ID of the sheet represented by this object.

This is an ID for the sheet that is unique to the spreadsheet. The ID is a monotonically
increasing integer assigned at sheet creation time that is independent of sheet position. This
is useful in conjunction with methods such as Range.copyFormatToRange(gridId, column, columnEnd, row, rowEnd) that take a gridId parameter rather than a Sheet instance.

**Returns:** Integer — An ID for the sheet unique to the spreadsheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

Logger.log(sheet.getSheetId());
```

### `getSheetName()`

Returns the sheet name.

**Returns:** String — The name of the sheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

Logger.log(sheet.getSheetName());
```

### `getSheetValues(startRow, startColumn, numRows, numColumns)`

Returns the rectangular grid of values for this range starting at the given coordinates. A -1
value given as the row or column position is equivalent to getting the very last row or column
that has data in the sheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| start Row | Integer | The position of the starting row. |
| start Column | Integer | The position of the starting column. |
| num Rows | Integer | The number of rows to return values for. |
| num Columns | Integer | The number of columns to return values for. |

**Returns:** Object[][] — A two-dimensional array of values.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// The two samples below produce the same output
let values = sheet.getSheetValues(1, 1, 3, 3);
Logger.log(values);

const range = sheet.getRange(1, 1, 3, 3);
values = range.getValues();
Logger.log(values);
```

### `getSheets()`

Gets all the sheets in this spreadsheet.

**Returns:** Sheet[] — An array of all the sheets in the spreadsheet.

```javascript
// The code below logs the name of the second sheet
const sheets = SpreadsheetApp.getActiveSpreadsheet().getSheets();
// Iterates through the sheets and logs the name and ID of each sheet.
for (const sheet of sheets) {
  Logger.log(`name: ${sheet.getName()}, ID: ${sheet.getSheetId()}`);
}
```

### `getSpreadsheetLocale()`

Gets the spreadsheet locale.

**Returns:** String — The spreadsheet locale.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets spreadsheet, you can use
// SpreadsheetApp.getActiveSpreadsheet() instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets the spreadsheet locale.
const ssLocale = ss.getSpreadsheetLocale();

// Logs the locale to the console.
console.log(ssLocale);
```

### `getSpreadsheetTheme()`

Returns the current theme of the spreadsheet, or null if no theme is applied.

**Returns:** SpreadsheetTheme |null — The current applied theme.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// The code below returns the current theme of the spreadsheet.
const currentTheme =
    SpreadsheetApp.getActiveSpreadsheet().getSpreadsheetTheme();
```

### `getSpreadsheetTimeZone()`

Gets the time zone for the spreadsheet.

**Returns:** String — The time zone, specified in "long" format (for example, "America/New_York", as listed
    by Joda.org ).

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets spreadsheet, you can use
// SpreadsheetApp.getActiveSpreadsheet() instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Sets the time zone of the spreadsheet.
ss.setSpreadsheetTimeZone('America/New_York');

// Gets the time zone of the spreadsheet.
const ssTimeZone = ss.getSpreadsheetTimeZone();

// Logs the time zone to the console.
console.log(ssTimeZone);
```

### `getUrl()`

Returns the URL for the given spreadsheet.

**Returns:** String — The URL for the given spreadsheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
Logger.log(ss.getUrl());
```

### `getViewers()`

Gets the list of viewers and commenters for this Spreadsheet .

**Returns:** User[] — An array of users with view or comment permission.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `hideColumn(column)`

Hides the column or columns in the given range.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| column | Range | The column range to hide. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// This hides the first column
let range = sheet.getRange('A1');
sheet.hideColumn(range);

// This hides the first 3 columns
range = sheet.getRange('A:C');
sheet.hideColumn(range);
```

### `hideRow(row)`

Hides the rows in the given range.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| row | Range | The row range to hide. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// This hides the first row
const range = sheet.getRange('A1');
sheet.hideRow(range);
```

### `insertColumnAfter(afterPosition)`

Inserts a column after the given column position.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| after Position | Integer | The column after which the new column should be added. |

**Returns:** Sheet — The sheet, useful for method chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// This inserts a column after the first column position
sheet.insertColumnAfter(1);
```

### `insertColumnBefore(beforePosition)`

Inserts a column before the given column position.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| before Position | Integer | The column before which the new column should be added. |

**Returns:** Sheet — The sheet, useful for method chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// This inserts a column in the first column position
sheet.insertColumnBefore(1);
```

### `insertColumnsAfter(afterPosition, howMany)`

Inserts a given number of columns after the given column position.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| after Position | Integer | The column after which the new column should be added. |
| how Many | Integer | The number of columns to insert. |

**Returns:** Sheet — The sheet, useful for method chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// Inserts two columns after the first column on the first sheet of the
// spreadsheet.
sheet.insertColumnsAfter(1, 2);
```

### `insertColumnsBefore(beforePosition, howMany)`

Inserts a number of columns before the given column position.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| before Position | Integer | The column before which the new column should be added. |
| how Many | Integer | The number of columns to insert. |

**Returns:** Sheet — The sheet, useful for method chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// This inserts five columns before the first column
sheet.insertColumnsBefore(1, 5);
```

### `insertDataSourceSheet(spec)`

Inserts a new DataSourceSheet in the spreadsheet and starts data execution. As a
side effect, this also makes the new sheet the active sheet.

Throws an exception if the data source type is not enabled. Use SpreadsheetApp#enable...Execution() methods to enable data execution for specific data source
type.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| spec | Data Source Spec | The data source specification to insert with. |

**Returns:** DataSourceSheet — The new data source sheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Activates BigQuery operations.
SpreadsheetApp.enableBigQueryExecution();

// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Builds a data source specification.
// TODO (developer): Update the project ID to your own Google Cloud project ID.
const dataSourceSpec = SpreadsheetApp.newDataSourceSpec()
                           .asBigQuery()
                           .setProjectId('project-id-1')
                           .setTableProjectId('bigquery-public-data')
                           .setDatasetId('ncaa_basketball')
                           .setTableId('mbb_historical_teams_games')
                           .build();

// Adds the data source and its data to the spreadsheet.
ss.insertDataSourceSheet(dataSourceSpec);
```

### `insertImage(blobSource, column, row)`

Inserts a Spreadsheet as an image in the document at a given row and column. The image
size is retrieved from the blob contents. The maximum supported blob size is 2MB.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| blob Source | Blob Source | The blob containing the image contents, MIME type, and (optionally) name. |
| column | Integer | The column position. |
| row | Integer | The row position. |

**Returns:** OverGridImage — The inserted image.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

const binaryData = [];  // TODO(developer): Replace with your binary data.
const blob = Utilities.newBlob(binaryData, 'image/png', 'MyImageName');
sheet.insertImage(blob, 1, 1);
```

### `insertImage(blobSource, column, row, offsetX, offsetY)`

Inserts a Spreadsheet as an image in the document at a given row and column, with a
pixel offset. The image size is retrieved from the blob contents. The maximum supported blob
size is 2MB.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| blob Source | Blob Source | The blob containing the image contents, MIME type, and (optionally) name. |
| column | Integer | The column position. |
| row | Integer | The row position. |
| offsetX | Integer | The horizontal offset from cell corner in pixels. |
| offsetY | Integer | The vertical offset from cell corner in pixels. |

**Returns:** OverGridImage — The inserted image.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

const binaryData = [];  // TODO(developer): Replace with your binary data.
const blob = Utilities.newBlob(binaryData, 'image/png', 'MyImageName');
sheet.insertImage(blob, 1, 1, 10, 10);
```

### `insertImage(url, column, row)`

Inserts an image in the document at a given row and column.

The provided URL must be publicly accessible.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| url | String | The URL of the image. |
| column | Integer | The grid column position. |
| row | Integer | The grid row position. |

**Returns:** OverGridImage — The inserted image.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

sheet.insertImage('https://www.google.com/images/srpr/logo3w.png', 1, 1);
```

### `insertImage(url, column, row, offsetX, offsetY)`

Inserts an image in the document at a given row and column, with a pixel offset.

The provided URL must be publicly accessible.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| url | String | The URL for the image. |
| column | Integer | The column position. |
| row | Integer | The row position. |
| offsetX | Integer | The horizontal offset from cell corner in pixels. |
| offsetY | Integer | The vertical offset from cell corner in pixels. |

**Returns:** OverGridImage — The Inserted image.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

sheet.insertImage(
    'https://www.google.com/images/srpr/logo3w.png',
    1,
    1,
    10,
    10,
);
```

### `insertRowAfter(afterPosition)`

Inserts a row after the given row position.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| after Position | Integer | The row after which the new row should be added. |

**Returns:** Sheet — The sheet, useful for method chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// This inserts a row after the first row position
sheet.insertRowAfter(1);
```

### `insertRowBefore(beforePosition)`

Inserts a row before the given row position.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| before Position | Integer | The row before which the new row should be added. |

**Returns:** Sheet — The sheet, useful for method chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// This inserts a row before the first row position
sheet.insertRowBefore(1);
```

### `insertRowsAfter(afterPosition, howMany)`

Inserts a number of rows after the given row position.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| after Position | Integer | The row after which the new rows should be added. |
| how Many | Integer | The number of rows to insert. |

**Returns:** Sheet — The sheet, useful for method chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// This inserts five rows after the first row
sheet.insertRowsAfter(1, 5);
```

### `insertRowsBefore(beforePosition, howMany)`

Inserts a number of rows before the given row position.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| before Position | Integer | The row before which the new rows should be added. |
| how Many | Integer | The number of rows to insert. |

**Returns:** Sheet — The sheet, useful for method chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// This inserts five rows before the first row
sheet.insertRowsBefore(1, 5);
```

### `insertSheet()`

Inserts a new sheet into the spreadsheet, using a default sheet name. The new sheet becomes the
active sheet.

**Returns:** Sheet — The new sheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
ss.insertSheet();
```

### `insertSheet(sheetIndex)`

Inserts a new sheet into the spreadsheet at the given index. The new sheet becomes the active
sheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| sheet Index | Integer | The index of the newly created sheet. To insert a sheet as the first one in
    the spreadsheet, set it to 0. |

**Returns:** Sheet — The new sheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
ss.insertSheet(1);
```

### `insertSheet(sheetIndex, options)`

Inserts a new sheet into the spreadsheet at the given index and uses optional advanced
arguments. The new sheet becomes the active sheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| sheet Index | Integer | The index of the newly created sheet. To insert a sheet as the first one in
    the spreadsheet, set it to 0. |
| options | Object | Optional JavaScript advanced arguments. |

**Returns:** Sheet — The new sheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const templateSheet = ss.getSheetByName('Sales');
ss.insertSheet(1, {template: templateSheet});
```

### `insertSheet(options)`

Inserts a new sheet into the spreadsheet, using a default sheet name and optional advanced
arguments. The new sheet becomes the active sheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| options | Object | Optional JavaScript advanced arguments, listed below. |

**Returns:** Sheet — The new sheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const templateSheet = ss.getSheetByName('Sales');
ss.insertSheet({template: templateSheet});
```

### `insertSheet(sheetName)`

Inserts a new sheet into the spreadsheet with the given name. The new sheet becomes the active
sheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| sheet Name | String | The name of the new sheet. |

**Returns:** Sheet — The new sheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
ss.insertSheet('My New Sheet');
```

### `insertSheet(sheetName, sheetIndex)`

Inserts a new sheet into the spreadsheet with the given name at the given index. The new sheet
becomes the active sheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| sheet Name | String | The name of the new sheet. |
| sheet Index | Integer | The index of the newly created sheet. To insert a sheet as the first one in
    the spreadsheet, set it to 0. |

**Returns:** Sheet — The new sheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
ss.insertSheet('My New Sheet', 1);
```

### `insertSheet(sheetName, sheetIndex, options)`

Inserts a new sheet into the spreadsheet with the given name at the given index and uses
optional advanced arguments. The new sheet becomes the active sheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| sheet Name | String | The name of the new sheet. |
| sheet Index | Integer | The index of the newly inserted sheet. To insert a sheet as the first one in
    a spreadsheet, set it to 0. |
| options | Object | Optional JavaScript advanced arguments. |

**Returns:** Sheet — The new sheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const templateSheet = ss.getSheetByName('Sales');
ss.insertSheet('My New Sheet', 1, {template: templateSheet});
```

### `insertSheet(sheetName, options)`

Inserts a new sheet into the spreadsheet with the given name and uses optional advanced
arguments. The new sheet becomes the active sheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| sheet Name | String | The name of the new sheet. |
| options | Object | Optional JavaScript advanced arguments. |

**Returns:** Sheet — The new sheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const templateSheet = ss.getSheetByName('Sales');
ss.insertSheet('My New Sheet', {template: templateSheet});
```

### `insertSheetWithDataSourceTable(spec)`

Inserts a new sheet in the spreadsheet, creates a DataSourceTable spanning the
entire sheet with the given data source specification, and starts data execution. As a side
effect, makes the new sheet the active sheet.

Throws an exception if the data source type is not enabled. Use SpreadsheetApp#enable...Execution() methods to enable data execution for specific data source
type.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| spec | Data Source Spec | The data source specification to insert with. |

**Returns:** Sheet — The new sheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Activates BigQuery operations.
SpreadsheetApp.enableBigQueryExecution();

// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Adds a sheet and sets cell A1 as the parameter cell.
const parameterCell = ss.insertSheet('parameterSheet').getRange('A1');

// Sets the value of the parameter cell to 'Duke'.
parameterCell.setValue('Duke');

const query = 'select * from `bigquery-public-data`.`ncaa_basketball`.' +
    '`mbb_historical_tournament_games` WHERE win_school_ncaa = @SCHOOL';

// Adds a data source with a query parameter.
// TODO(developer): Update the project ID to your own Google Cloud project ID.
const dataSourceSpec = SpreadsheetApp.newDataSourceSpec()
                           .asBigQuery()
                           .setProjectId('project-id-1')
                           .setRawQuery(query)
                           .setParameterFromCell('SCHOOL', 'parameterSheet!A1')
                           .build();

// Adds sheets for the data source and data source table to the spreadsheet.
ss.insertSheetWithDataSourceTable(dataSourceSpec);
```

### `isColumnHiddenByUser(columnPosition)`

Returns whether the given column is hidden by the user.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| column Position | Integer | The position of the column to examine. |

**Returns:** Boolean — true if the column is hidden, false otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// Columns start at 1
Logger.log(sheet.isColumnHiddenByUser(1));
```

### `isIterativeCalculationEnabled()`

Returns whether iterative calculation is activated in this spreadsheet.

**Returns:** Boolean — true if iterative calculation is activated, false otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets spreadsheet, you can use
// SpreadsheetApp.getActiveSpreadsheet() instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Activates iterative calculation on the spreadsheet.
ss.setIterativeCalculationEnabled(true);

// Logs whether iterative calculation is activated for the spreadsheet.
console.log(ss.isIterativeCalculationEnabled());
```

### `isRowHiddenByFilter(rowPosition)`

Returns whether the given row is hidden by a filter (not a filter view).

**Parameters:**

| Name | Type | Description |
|---|---|---|
| row Position | Integer | The position of the row to examine. |

**Returns:** Boolean — true if the row is hidden, false otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// Rows start at 1
Logger.log(sheet.isRowHiddenByFilter(1));
```

### `isRowHiddenByUser(rowPosition)`

Returns whether the given row is hidden by the user.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| row Position | Integer | The position of the row to examine. |

**Returns:** Boolean — true if the row is hidden, false otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// Rows start at 1
Logger.log(sheet.isRowHiddenByUser(1));
```

### `moveActiveSheet(pos)`

Moves the active sheet to the given position in the list of sheets. Throws an exception if the
position is negative or greater than the number of sheets.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| pos | Integer | The 1-index position to move the active sheet to in the list of sheets. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// This example assumes that there are 2 sheets in the current
// active spreadsheet: one named "first" in position 1 and another named
// "second" in position 2.
const spreadsheet = SpreadsheetApp.getActiveSpreadsheet();
// Gets the "first" sheet and activates it.
const sheet = spreadsheet.getSheetByName('first').activate();

// Logs 'Current index of sheet: 1'
console.log('Current index of sheet: %s', sheet.getIndex());

spreadsheet.moveActiveSheet(2);

// Logs 'New index of sheet: 2'
console.log('New index of sheet: %s', sheet.getIndex());
```

### `moveChartToObjectSheet(chart)`

Creates a new SheetType.OBJECT sheet and moves the provided chart to it. If the chart
is already on its own sheet, that sheet is returned without creating a new one.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| chart | Embedded Chart | The chart to move. |

**Returns:** Sheet — The sheet that the chart is on.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const chart = sheet.newChart().setPosition(1, 1, 0, 0).build();
sheet.insertChart(chart);
const objectSheet = SpreadsheetApp.getActive().moveChartToObjectSheet(chart);
```

### `refreshAllDataSources()`

Refreshes all supported data sources and their linked data source objects, skipping invalid
data source objects.

Use SpreadsheetApp#enable...Execution() methods to enable data execution for
specific data source type.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Activates BigQuery operations.
SpreadsheetApp.enableBigQueryExecution();

// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets file, you can use SpreadsheetApp.getActiveSpreadsheet()
// instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Gets the first data source sheet on the spreadsheet.
const dataSheet = ss.getDataSourceSheets()[0];

// Refreshes all data sources on the spreadsheet.
ss.refreshAllDataSources();

// Logs the last refreshed time of the first data source sheet.
console.log(
    `Last refresh time: ${dataSheet.getStatus().getLastRefreshedTime()}`,
);
```

### `removeEditor(emailAddress)`

Removes the given user from the list of editors for the Spreadsheet . This method doesn't
block users from accessing the Spreadsheet if they belong to a class of users who have
general access—for example, if the Spreadsheet is shared with the user's entire
domain, or if the Spreadsheet is in a shared drive that the user can access.

For Drive files, this also removes the user from the list of viewers.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| email Address | String | The email address of the user to remove. |

**Returns:** Spreadsheet — This Spreadsheet , for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `removeEditor(user)`

Removes the given user from the list of editors for the Spreadsheet . This method doesn't
block users from accessing the Spreadsheet if they belong to a class of users who have
general access—for example, if the Spreadsheet is shared with the user's entire
domain, or if the Spreadsheet is in a shared drive that the user can access.

For Drive files, this also removes the user from the list of viewers.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| user | User | A representation of the user to remove. |

**Returns:** Spreadsheet — This Spreadsheet , for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `removeMenu(name)`

Removes a menu that was added by addMenu(name, subMenus) . The name argument
should have the same value as the corresponding call to addMenu(name, subMenus) .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| name | String | The name of the menu to remove. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// The onOpen function is executed automatically every time a Spreadsheet is
// loaded
function onOpen() {
  const ss = SpreadsheetApp.getActiveSpreadsheet();
  ss.addMenu('badMenu', [
    {name: 'remove bad menu', functionName: 'removeBadMenu'},
    {name: 'foo', functionName: 'foo'},
  ]);
}
function removeBadMenu() {
  const ss = SpreadsheetApp.getActiveSpreadsheet();
  ss.removeMenu(
      'badMenu');  // name must match the name used when added the menu
}
function foo() {
  // Do nothing
}
```

### `removeNamedRange(name)`

Deletes a named range with the given name. Throws an exception if no range with the given name
is found in the spreadsheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| name | String | The range name. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// The code below creates a new named range "foo", and then remove it.
const ss = SpreadsheetApp.getActiveSpreadsheet();
ss.setNamedRange('foo', ss.getActiveRange());
ss.removeNamedRange('foo');
```

### `removeViewer(emailAddress)`

Removes the given user from the list of viewers and commenters for the Spreadsheet . This
method has no effect if the user is an editor, not a viewer or commenter. This method also
doesn't block users from accessing the Spreadsheet if they belong to a class of users who
have general access—for example, if the Spreadsheet is shared with the user's
entire domain, or if the Spreadsheet is in a shared drive that the user can access.

For Drive files, this also removes the user from the list of editors.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| email Address | String | The email address of the user to remove. |

**Returns:** Spreadsheet — This Spreadsheet for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `removeViewer(user)`

Removes the given user from the list of viewers and commenters for the Spreadsheet . This
method has no effect if the user is an editor, not a viewer. This method also doesn't block
users from accessing the Spreadsheet if they belong to a class of users who have general
access—for example, if the Spreadsheet is shared with the user's entire domain, or
if the Spreadsheet is in a shared drive that the user can access.

For Drive files, this also removes the user from the list of editors.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| user | User | A representation of the user to remove. |

**Returns:** Spreadsheet — This Spreadsheet for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `rename(newName)`

Renames the document.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| new Name | String | The new name for the document. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
ss.rename('This is the new name');
```

### `renameActiveSheet(newName)`

Renames the current active sheet to the given new name.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| new Name | String | The new name for the current active sheet. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// The code below renames the active sheet to "Hello world"
SpreadsheetApp.getActiveSpreadsheet().renameActiveSheet('Hello world');
```

### `resetSpreadsheetTheme()`

Removes the applied theme and sets the default theme on the spreadsheet.

**Returns:** SpreadsheetTheme — The default theme.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// The code below applies default theme on the spreadsheet.
SpreadsheetApp.getActiveSpreadsheet().resetSpreadsheetTheme();
```

### `setActiveRange(range)`

Sets the specified range as the active range in the active sheet, with
the top left cell in the range as the current cell .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| range | Range | The range to set as the active range. |

**Returns:** Range — The newly active range.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
const range = sheet.getRange('A1:D4');
sheet.setActiveRange(range);

const selection = sheet.getSelection();
// Current cell: A1
const currentCell = selection.getCurrentCell();
// Active Range: A1:D4
const activeRange = selection.getActiveRange();
```

### `setActiveRangeList(rangeList)`

Sets the specified list of ranges as the active ranges in the
active sheet. The last range in the list is set as the active range .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| range List | Range List | The list of ranges to select. |

**Returns:** RangeList — The newly selected list of ranges.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['D4', 'B2:C4']);
sheet.setActiveRangeList(rangeList);

const selection = sheet.getSelection();
// Current cell: B2
const currentCell = selection.getCurrentCell();
// Active range: B2:C4
const activeRange = selection.getActiveRange();
// Active range list: [D4, B2:C4]
const activeRangeList = selection.getActiveRangeList();
```

### `setActiveSelection(range)`

Sets the active selection region for this sheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| range | Range | The range to set as the active selection. |

**Returns:** Range — The newly active range.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

const range = sheet.getRange('A1:D4');
sheet.setActiveSelection(range);
```

### `setActiveSelection(a1Notation)`

Sets the active selection, as specified in A1 notation or R1C1 notation.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| a1Notation | String | The range to set as active, as specified in A1 notation or R1C1 notation. |

**Returns:** Range — The newly active range.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

sheet.setActiveSelection('A1:D4');
```

### `setActiveSheet(sheet)`

Sets the given sheet to be the active sheet in the spreadsheet. The Google Sheets UI displays
the chosen sheet unless the sheet belongs to a different spreadsheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| sheet | Sheet | The sheet to set as the active sheet. |

**Returns:** Sheet — The active sheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// The code below makes the first sheet active in the active spreadsheet.
const spreadsheet = SpreadsheetApp.getActiveSpreadsheet();
spreadsheet.setActiveSheet(spreadsheet.getSheets()[0]);
```

### `setActiveSheet(sheet, restoreSelection)`

Sets the given sheet to be the active sheet in the spreadsheet, with an option to restore the
most recent selection within that sheet. The Google Sheets UI displays the chosen sheet unless
the sheet belongs to a different spreadsheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| sheet | Sheet | The new active sheet. |
| restore Selection | Boolean | Tf true , the most recent selection of the new active sheet
    becomes selected again as the new sheet becomes active; if false , the new sheet
    becomes active without changing the current selection. |

**Returns:** Sheet — The new active sheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const spreadsheet = SpreadsheetApp.getActiveSpreadsheet();
const firstSheet = spreadsheet.getSheets()[0];
const secondSheet = spreadsheet.getSheets()[1];
// Set the first sheet as the active sheet and select the range D4:F4.
spreadsheet.setActiveSheet(firstSheet).getRange('D4:F4').activate();

// Switch to the second sheet to do some work.
spreadsheet.setActiveSheet(secondSheet);
// Switch back to first sheet, and restore its selection.
spreadsheet.setActiveSheet(firstSheet, true);

// The selection of first sheet is restored, and it logs D4:F4
const range = spreadsheet.getActiveSheet().getSelection().getActiveRange();
Logger.log(range.getA1Notation());
```

### `setColumnWidth(columnPosition, width)`

Sets the width of the given column in pixels.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| column Position | Integer | The position of the given column to set. |
| width | Integer | The width in pixels to set it to. |

**Returns:** Sheet — The sheet, useful for method chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// Sets the first column to a width of 200 pixels
sheet.setColumnWidth(1, 200);
```

### `setCurrentCell(cell)`

Sets the specified cell as the current cell .

If the specified cell is present in an already selected range, then that range becomes the
active range with the cell as the current cell.

If the specified cell is not present in any selected range, then any existing selection is
removed and the cell becomes the current cell and the active range.

Note: The specified Range must consist of one cell, otherwise it throws an
exception.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| cell | Range | The cell to set as the current cell. |

**Returns:** Range — The newly set current cell.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
const cell = sheet.getRange('B5');
sheet.setCurrentCell(cell);

const selection = sheet.getSelection();
// Current cell: B5
const currentCell = selection.getCurrentCell();
```

### `setFrozenColumns(columns)`

Freezes the given number of columns. If zero, no columns are frozen.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| columns | Integer | The number of columns to freeze. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// Freezes the first column
sheet.setFrozenColumns(1);
```

### `setFrozenRows(rows)`

Freezes the given number of rows. If zero, no rows are frozen.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| rows | Integer | The number of rows to freeze. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// Freezes the first row
sheet.setFrozenRows(1);
```

### `setIterativeCalculationConvergenceThreshold(minThreshold)`

Sets the minimum threshold value for iterative calculation. When the results of successive
calculation differ by less than this value, the iterative calculation stops. This value must be
non-negative, and defaults to 0.05.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| min Threshold | Number | The minimum convergence threshold (must be non-negative). |

**Returns:** Spreadsheet — This spreadsheet, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets spreadsheet, you can use
// SpreadsheetApp.getActiveSpreadsheet() instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Sets the iterative calculation convergence threshold for the spreadsheet.
ss.setIterativeCalculationConvergenceThreshold(2);

// Logs the threshold to the console.
console.log(ss.getIterativeCalculationConvergenceThreshold());
```

### `setIterativeCalculationEnabled(isEnabled)`

Sets whether iterative calculation is activated in this spreadsheet. If the maximum number of
calculation cycles and convergence threshold have not previously been set when the calculation
is activated, they default to 50 and 0.05 respectively. If either has been set previously, they
retain their previous values.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| is Enabled | Boolean | true if iterative calculation should be enabled; false otherwise. |

**Returns:** Spreadsheet — This spreadsheet, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets spreadsheet, you can use
// SpreadsheetApp.getActiveSpreadsheet() instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Activates iterative calculation on the spreadsheet.
ss.setIterativeCalculationEnabled(true);

// Logs whether iterative calculation is activated for the spreadsheet.
console.log(ss.isIterativeCalculationEnabled());
```

### `setMaxIterativeCalculationCycles(maxIterations)`

Sets the maximum number of calculation iterations that should be performed during iterative
calculation. This value must be between 1 and 10,000 (inclusive), and defaults to 50.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| max Iterations | Integer | The maximum number of calculation iterations (between 1 and 10,000). |

**Returns:** Spreadsheet — This spreadsheet, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets spreadsheet, you can use
// SpreadsheetApp.getActiveSpreadsheet() instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Sets the max iterative calculation cycles for the spreadsheet.
ss.setMaxIterativeCalculationCycles(10);

// Logs the max iterative calculation cycles to the console.
console.log(ss.getMaxIterativeCalculationCycles());
```

### `setNamedRange(name, range)`

Names a range.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| name | String | The name to give the range. |
| range | Range | The range specification. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// The code below creates a new named range "TaxRates" in the active spreadsheet
const ss = SpreadsheetApp.getActiveSpreadsheet();
ss.setNamedRange('TaxRates', SpreadsheetApp.getActiveRange());
```

### `setRecalculationInterval(recalculationInterval)`

Sets how often this spreadsheet should recalculate.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| recalculation Interval | Recalculation Interval | The new recalculation interval. |

**Returns:** Spreadsheet — This spreadsheet, for chaining.

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

// Sets the  calculation interval for the spreadsheet to 'ON_CHANGE'.
const interval = ss.setRecalculationInterval(
    SpreadsheetApp.RecalculationInterval.ON_CHANGE,
);

// Logs the calculation interval to the console.
console.log(interval);
```

### `setRowHeight(rowPosition, height)`

Sets the row height of the given row in pixels. By default, rows grow to fit cell contents. If
you want to force rows to a specified height, use Sheet.setRowHeightsForced(startRow, numRows, height) .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| row Position | Integer | The row position to change. |
| height | Integer | The height in pixels to set it to. |

**Returns:** Sheet — The sheet, useful for method chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// Sets the first row to a height of 200 pixels
sheet.setRowHeight(1, 200);
```

### `setSpreadsheetLocale(locale)`

Sets the spreadsheet locale.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| locale | String | The locale code to use (for example, 'en', 'fr', or 'en_US'). |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets spreadsheet, you can use
// SpreadsheetApp.getActiveSpreadsheet() instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Sets the spreadsheet locale.
ss.setSpreadsheetLocale('fr');

// Gets the spreadsheet locale.
const ssLocale = ss.getSpreadsheetLocale();

// Logs the locale to the console.
console.log(ssLocale);
```

### `setSpreadsheetTheme(theme)`

Sets a theme on the spreadsheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| theme | Spreadsheet Theme | The theme to apply. |

**Returns:** SpreadsheetTheme — The new current theme.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const spreadsheet = SpreadsheetApp.getActiveSpreadsheet();
// The code below sets the second predefined theme as the current theme of the
// spreadsheet.
const predefinedThemesList = spreadsheet.getPredefinedSpreadsheetThemes();
spreadsheet.setSpreadsheetTheme(predefinedThemesList[1]);
```

### `setSpreadsheetTimeZone(timezone)`

Sets the time zone for the spreadsheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| timezone | String | The time zone, specified in "long" format (for example, "America/New_York", as
    listed by Joda.org ). |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Opens the spreadsheet file by its URL. If you created your script from within
// a Google Sheets spreadsheet, you can use
// SpreadsheetApp.getActiveSpreadsheet() instead.
// TODO(developer): Replace the URL with your own.
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);

// Sets the time zone of the spreadsheet.
ss.setSpreadsheetTimeZone('America/New_York');

// Gets the time zone of the spreadsheet.
const ssTimeZone = ss.getSpreadsheetTimeZone();

// Logs the time zone to the console.
console.log(ssTimeZone);
```

### `show(userInterface)`

Displays a custom user interface component in a dialog centered in the user's browser's
viewport. The server-side script's execution is not suspended. To communicate with the
server side, the user interface component must make asynchronous callbacks to the server-side
script.

If the server-side script previously displayed a dialog that has not yet been dismissed,
then the existing dialog is replaced with the newly requested dialog's user interface.

The following code snippet displays a simple HtmlService application in a dialog with the
specified title, height, and width:

**Parameters:**

| Name | Type | Description |
|---|---|---|
| user Interface | Object | An Html Output . |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.container.ui`

```javascript
const htmlApp = HtmlService
                    .createHtmlOutput(
                        '<p>A change of speed, a change of style...</p>',
                        )
                    .setTitle('My HtmlService Application')
                    .setWidth(250)
                    .setHeight(300);

SpreadsheetApp.getActiveSpreadsheet().show(htmlApp);

// The script resumes execution immediately after showing the dialog.
```

### `sort(columnPosition)`

Sorts a sheet by column, ascending.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| column Position | Integer | The column to sort by. |

**Returns:** Sheet — The sheet, useful for method chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// Sorts the sheet by the first column, ascending
sheet.sort(1);
```

### `sort(columnPosition, ascending)`

Sorts a sheet by column. Takes a parameter to specify ascending or descending.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| column Position | Integer | The column to sort by. |
| ascending | Boolean | true for ascending sorts, false for descending. |

**Returns:** Sheet — The sheet, useful for method chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// Sorts the sheet by the first column, descending
sheet.sort(1, false);
```

### `toast(msg)`

Shows a popup window in the lower right corner of the spreadsheet with the given message.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| msg | String | The message to be shown in the toast. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Show a popup with the message "Task started".
SpreadsheetApp.getActiveSpreadsheet().toast('Task started');
```

### `toast(msg, title)`

Shows a popup window in the lower right corner of the spreadsheet with the given message and
title.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| msg | String | The message to be shown in the toast. |
| title | String | The optional title of the toast. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Show a popup with the title "Status" and the message "Task started".
SpreadsheetApp.getActiveSpreadsheet().toast('Task started', 'Status');
```

### `toast(msg, title, timeoutSeconds)`

Shows a popup window in the lower right corner of the spreadsheet with the given title and
message, that stays visible for a certain length of time.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| msg | String | The message to be shown in the toast. |
| title | String | The optional title of the toast. |
| timeout Seconds | Number | The timeout in seconds; if null , the toast defaults to 5 seconds;
    if negative, the toast remains until dismissed. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Show a 3-second popup with the title "Status" and the message "Task started".
SpreadsheetApp.getActiveSpreadsheet().toast('Task started', 'Status', 3);
```

### `unhideColumn(column)`

Unhides the column in the given range.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| column | Range | The range to unhide, if hidden. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// This unhides the first column if it was previously hidden
const range = sheet.getRange('A1');
sheet.unhideColumn(range);
```

### `unhideRow(row)`

Unhides the row in the given range.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| row | Range | The range to unhide, if hidden. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// This unhides the first row if it was previously hidden
const range = sheet.getRange('A1');
sheet.unhideRow(range);
```

### `updateMenu(name, subMenus)`

Updates a menu that was added by addMenu(name, subMenus) . Works exactly like addMenu(name, subMenus) .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| name | String | The name of the menu to update. |
| sub Menus | Object[] | An array of JavaScript maps with name and function Name parameters. You can use functions from included libraries, such as Library.libFunction1 . |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const menuEntries = [];
menuEntries.push({name: 'Lone Menu Entry', functionName: 'function1'});
ss.updateMenu('addMenuExample', menuEntries);
```

### `waitForAllDataExecutionsCompletion(timeoutInSeconds)`

Waits until all the current executions in the spreadsheet complete, timing out after the
provided number of seconds. Throws an exception if the executions are not completed when timing
out, but does not cancel the data executions.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| timeout In Seconds | Integer | The time to wait for data executions, in seconds. The maximum is 300
    seconds. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

## Deprecated Methods

### `getSheetProtection()`

Deprecated. For spreadsheets created in the newer version of Google Sheets, use Sheet.getProtections(type) , which returns the more powerful Protection class. Although this method is deprecated, it remains available for
    compatibility with the older version of Sheets

Returns a PageProtection instance describing the permissions for the current sheet.

**Returns:** PageProtection — An object describing sheet access permissions.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

const permissions = sheet.getSheetProtection();

permissions.setProtected(true);
permissions.addUser('user@example.com');

// Logs the users that have access to edit this sheet. Note that this
// is different from access to the entire spreadsheet - getUsers()
// only returns users if permissions.isProtected() is set to true.
const users = permissions.getUsers();
Logger.log(users);
```

### `isAnonymousView()`

Deprecated. As of January 2014 this function is deprecated and not available in the new version
    of Google Sheets.

Indicates whether the document allows anonymous viewing. As this is no longer supported in the new version of Google Sheets , use File.getSharingAccess() and File.getSharingPermission() instead.

**Returns:** Boolean — true if the document allows anonymous viewing, false otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Determine if the document allows anonymous viewing via the Drive API.
const ss = SpreadsheetApp.getActiveSpreadsheet();
const file = DriveApp.getFileById(ss.getId());
const access = file.getSharingAccess();
const permission = file.getSharingPermission();
const isAnonymousAccess = access === DriveApp.Access.ANYONE ||
    access === DriveApp.Access.ANYONE_WITH_LINK;
const isAnonymousEdit =
    isAnonymousAccess && permission !== DriveApp.Permission.NONE;
```

### `isAnonymousWrite()`

Deprecated. As of January 2014 this function is deprecated and not available in the new version
    of Google Sheets.

Indicates whether the document allows edits from anonymous users. As this is no longer
supported in the new version of
Google Sheets , use File.getSharingAccess() and File.getSharingPermission() instead.

**Returns:** Boolean — true if the document allows anonymous editing, false otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Determine if the document allow anonymous edits via the Drive API.
const ss = SpreadsheetApp.getActiveSpreadsheet();
const file = DriveApp.getFileById(ss.getId());
const access = file.getSharingAccess();
const permission = file.getSharingPermission();
const isAnonymousAccess = access === DriveApp.Access.ANYONE ||
    access === DriveApp.Access.ANYONE_WITH_LINK;
const isAnonymousEdit =
    isAnonymousAccess && permission === DriveApp.Permission.EDIT;
```

### `setAnonymousAccess(anonymousReadAllowed, anonymousWriteAllowed)`

Deprecated. As of January 2014 this function is deprecated and not available in the new version
    of Google Sheets.

Sets the document's policy on anonymous reading and writing. As this is no longer supported in
the new version of Google Sheets ,
use File.setSharing(accessType, permissionType) as an alternative.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| anonymous Read Allowed | Boolean | true to allow anonymous reads; false otherwise. |
| anonymous Write Allowed | Boolean | true to allow anonymous reads; false otherwise. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Set the document's policy on anonymous reading and writing via the Drive API.
const ss = SpreadsheetApp.getActiveSpreadsheet();
const file = DriveApp.getFileById(ss.getId());

// Set anonymous read.
file.setSharing(DriveApp.Access.ANYONE, DriveApp.Permission.VIEW);

// Set anonymous write.
file.setSharing(DriveApp.Access.ANYONE, DriveApp.Permission.EDIT);

// Disable anonymous access.
file.setSharing(DriveApp.Access.PRIVATE, file.getSharingPermission());
```

### `setSheetProtection(permissions)`

Deprecated. For spreadsheets created in the newer version of Google Sheets, use Sheet.protect() , which returns the more powerful Protection class. Although
    this method is deprecated, it remains available for compatibility with the older version of
    Sheets

Sets the permissions for the current sheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| permissions | Page Protection | The access permissions object to set on this sheet. |

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

const permissions = sheet.getSheetProtection();

// This copies the permissions on the first sheet to the second sheet
const sheetToClonePermissionsTo = ss.getSheets()[1];
sheetToClonePermissionsTo.setSheetProtection(permissions);
```

