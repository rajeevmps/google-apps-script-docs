# TriggerBuilder

A generic builder for script triggers.

A generic builder for script triggers.

## Methods

### forDocument(document: Document) → DocumentTriggerBuilder

Creates and returns a `DocumentTriggerBuilder` tied to the given document.

**Parameters:**
- `document` (`Document`): The document.

**Return:** `DocumentTriggerBuilder` — The new DocumentTriggerBuilder.

**Authorization:** Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`.

```javascript
ScriptApp.newTrigger('myFunction')
    .forDocument(DocumentApp.getActiveDocument())
    .onOpen()
    .create();
```

### forDocument(key: String) → DocumentTriggerBuilder

Creates and returns a `DocumentTriggerBuilder` tied to the document with the given ID.

**Parameters:**
- `key` (`String`): The ID for the document.

**Return:** `DocumentTriggerBuilder` — The new DocumentTriggerBuilder.

**Authorization:** Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`.

```javascript
ScriptApp.newTrigger('myFunction')
    .forDocument('1234567890abcdefghijklmnopqrstuvwxyz')
    .onOpen()
    .create();
```

### forForm(form: Form) → FormTriggerBuilder

Creates and returns a `FormTriggerBuilder` tied to the given form.

**Parameters:**
- `form` (`Form`): The form.

**Return:** `FormTriggerBuilder` — The new FormTriggerBuilder.

**Authorization:** Requires `https://www.googleapis.com/auth/forms.currentonly` or `https://www.googleapis.com/auth/forms`.

```javascript
ScriptApp.newTrigger('myFunction')
    .forForm(FormApp.getActiveForm())
    .onFormSubmit()
    .create();
```

### forForm(key: String) → FormTriggerBuilder

Creates and returns a `FormTriggerBuilder` tied to the form with the given ID.

**Parameters:**
- `key` (`String`): The ID for the form.

**Return:** `FormTriggerBuilder` — The new FormTriggerBuilder.

**Authorization:** Requires `https://www.googleapis.com/auth/forms.currentonly` or `https://www.googleapis.com/auth/forms`.

```javascript
ScriptApp.newTrigger('myFunction')
    .forForm('1234567890abcdefghijklmnopqrstuvwxyz')
    .onFormSubmit()
    .create();
```

### forSpreadsheet(sheet: Spreadsheet) → SpreadsheetTriggerBuilder

Creates and returns a `SpreadsheetTriggerBuilder` tied to the given spreadsheet.

**Parameters:**
- `sheet` (`Spreadsheet`): The spreadsheet.

**Return:** `SpreadsheetTriggerBuilder` — The new SpreadsheetTriggerBuilder.

**Authorization:** Requires `https://www.googleapis.com/auth/spreadsheets.currentonly` or `https://www.googleapis.com/auth/spreadsheets`.

```javascript
ScriptApp.newTrigger('myFunction')
    .forSpreadsheet(SpreadsheetApp.getActive())
    .onEdit()
    .create();
```

### forSpreadsheet(key: String) → SpreadsheetTriggerBuilder

Creates and returns a `SpreadsheetTriggerBuilder` tied to the spreadsheet with the given ID.

**Parameters:**
- `key` (`String`): The ID for the spreadsheet.

**Return:** `SpreadsheetTriggerBuilder` — The new SpreadsheetTriggerBuilder.

**Authorization:** Requires `https://www.googleapis.com/auth/spreadsheets.currentonly` or `https://www.googleapis.com/auth/spreadsheets`.

```javascript
ScriptApp.newTrigger('myFunction')
    .forSpreadsheet('1234567890abcdefghijklmnopqrstuvwxyz')
    .onEdit()
    .create();
```

### forUserCalendar(emailId: String) → CalendarTriggerBuilder

Returns a builder for building calendar triggers.

**Parameters:**
- `emailId` (`String`): Email ID of the user calendar the trigger monitors.

**Return:** `CalendarTriggerBuilder` — The new CalendarTriggerBuilder.

**Authorization:** Requires calendar-related scopes including `https://www.googleapis.com/auth/calendar`.

### timeBased() → ClockTriggerBuilder

Creates and returns a `ClockTriggerBuilder` for building time-based triggers.

**Return:** `ClockTriggerBuilder` — The new ClockTriggerBuilder.

**Authorization:** Requires `https://www.googleapis.com/auth/script.scriptapp`.

```javascript
ScriptApp.newTrigger('myFunction').timeBased().atDate(2013, 10, 31).create();
```
