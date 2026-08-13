# DestinationType

An enum representing the supported types of form-response destinations.

An enum representing the supported types of form-response destinations. All forms, including those that do not have a destination set explicitly, save a copy of responses in the form's response store.

Destination types are accessed via `FormApp.DestinationType`.

## Code Sample

```javascript
// Open a form by ID and create a new spreadsheet.
const form = FormApp.openById('1234567890abcdefghijklmnopqrstuvwxyz');
const ss = SpreadsheetApp.create('Spreadsheet Name');

// Update the form's response destination.
form.setDestination(FormApp.DestinationType.SPREADSHEET, ss.getId());
```

## Properties

| Property | Description |
| --- | --- |
| `SPREADSHEET` | A Google Sheets spreadsheet as a destination for form responses. |
