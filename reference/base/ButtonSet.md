# ButtonSet

An enum representing predetermined, localized sets of one or more dialog buttons that can be added to an alert or a prompt.

An enum representing predetermined, localized sets of one or more dialog buttons that can be added to an alert or a prompt. To determine which button the user clicked, use Button.

To call an enum, you call its parent class, name, and property. For example, `Base.ButtonSet.OK`.

## Code Sample

```javascript
const ui = DocumentApp.getUi();
const response = ui.alert(
    'Are you sure you want to continue?',
    ui.ButtonSet.YES_NO,
);

if (response === ui.Button.YES) {
  Logger.log('The user clicked "Yes."');
} else {
  Logger.log('The user clicked "No" or the dialog\'s close button.');
}
```

## Properties

| Property | Description |
|----------|-------------|
| `OK` | A single "OK" button, indicating an informational message that can only be dismissed. |
| `OK_CANCEL` | An "OK" button and a "Cancel" button, allowing the user to either proceed with or halt an operation. |
| `YES_NO` | A "Yes" button and a "No" button, allowing the user to answer a yes/no question. |
| `YES_NO_CANCEL` | A "Yes" button, a "No" button, and a "Cancel" button, allowing the user to either answer a yes/no question or halt an operation. |
