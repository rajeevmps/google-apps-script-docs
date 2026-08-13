# Button

An enum representing predetermined, localized dialog buttons returned by an alert or PromptResponse.getSelectedButton().

An enum representing predetermined, localized dialog buttons returned by an `alert` or `PromptResponse.getSelectedButton()` to indicate which button in a dialog the user clicked.

These values cannot be set; to add buttons to an `alert` or `prompt`, use `ButtonSet` instead.

## Code Sample

```javascript
// Display a dialog box with a message and "Yes" and "No" buttons.
const ui = DocumentApp.getUi();
const response = ui.alert(
    'Are you sure you want to continue?',
    ui.ButtonSet.YES_NO,
);

// Process the user's response.
if (response === ui.Button.YES) {
  Logger.log('The user clicked "Yes."');
} else {
  Logger.log('The user clicked "No" or the dialog\'s close button.');
}
```

## Properties

| Property | Description |
|----------|-------------|
| `CLOSE` | The standard close button displayed in every dialog's title bar. This button is not explicitly added to a dialog, and it cannot be removed. |
| `OK` | An "OK" button, indicating that an operation should proceed. |
| `CANCEL` | A "Cancel" button, indicating that an operation should not proceed. |
| `YES` | A "Yes" button, indicating a positive response to a question. |
| `NO` | A "No" button, indicating a negative response to a question. |
