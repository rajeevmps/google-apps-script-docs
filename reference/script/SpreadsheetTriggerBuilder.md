# SpreadsheetTriggerBuilder

Builder for spreadsheet triggers.

Builder for spreadsheet triggers.

## Methods

### create() → Trigger

Creates the trigger and returns it.

**Return:** `Trigger` — The created trigger.

### onChange() → SpreadsheetTriggerBuilder

Specifies a trigger that fires when the spreadsheet's content or structure is changed.

**Return:** `SpreadsheetTriggerBuilder` — A builder for chaining.

```javascript
const sheet = SpreadsheetApp.getActive();
ScriptApp.newTrigger('myFunction').forSpreadsheet(sheet).onChange().create();
```

### onEdit() → SpreadsheetTriggerBuilder

Specifies a trigger that fires when the spreadsheet is edited.

**Return:** `SpreadsheetTriggerBuilder` — A builder for chaining.

```javascript
const sheet = SpreadsheetApp.getActive();
ScriptApp.newTrigger('myFunction').forSpreadsheet(sheet).onEdit().create();
```

### onFormSubmit() → SpreadsheetTriggerBuilder

Specifies a trigger that fires when the spreadsheet has a form submitted to it.

**Return:** `SpreadsheetTriggerBuilder` — A builder for chaining.

```javascript
const sheet = SpreadsheetApp.getActive();
ScriptApp.newTrigger('myFunction').forSpreadsheet(sheet).onFormSubmit().create();
```

### onOpen() → SpreadsheetTriggerBuilder

Specifies a trigger that fires when the spreadsheet is opened.

**Return:** `SpreadsheetTriggerBuilder` — A builder for chaining.

```javascript
const sheet = SpreadsheetApp.getActive();
ScriptApp.newTrigger('myFunction').forSpreadsheet(sheet).onOpen().create();
```
