# Browser

This class provides access to dialog boxes specific to Google Sheets.

This class provides access to dialog boxes specific to Google Sheets. The methods in this class are only available for use in the context of a Google Spreadsheet.

## Methods

### inputBox(prompt: String) → String

Pops up a dialog box with a text input box in the user's browser.

**Note:** This method is not recommended; use the Google Workspace dialog services (e.g. `Ui` class) instead.

### inputBox(prompt: String, buttons: Button) → String

Pops up a dialog box with a text input box in the user's browser.

**Note:** This method is not recommended; use the Google Workspace dialog services instead.

### inputBox(title: String, prompt: String, buttons: Button) → String

Pops up a dialog box with a text input box in the user's browser.

**Note:** This method is not recommended; use the Google Workspace dialog services instead.

### msgBox(prompt: String) → String

Pops up a dialog box with the given message and an OK button in the user's browser.

**Note:** This method is not recommended; use the Google Workspace dialog services instead.

### msgBox(prompt: String, buttons: Button) → String

Pops up a dialog box with the given message and specified buttons.

**Note:** This method is not recommended; use the Google Workspace dialog services instead.

### msgBox(title: String, prompt: String, buttons: Button) → String

Pops up a dialog box with the given title, message and specified buttons.

**Note:** This method is not recommended; use the Google Workspace dialog services instead.

## Code Sample

```javascript
const name = Browser.inputBox('Enter your name');
const name = Browser.inputBox('Enter your name', Browser.Buttons.OK_CANCEL);
const name = Browser.inputBox('ID Check', 'Enter your name', Browser.Buttons.OK_CANCEL);
Browser.msgBox('hello world');
Browser.msgBox('hello world', Browser.Buttons.OK_CANCEL);
Browser.msgBox('Greetings', 'hello world', Browser.Buttons.YES_NO);
```
