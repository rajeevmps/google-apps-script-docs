# Ui

An instance of the user-interface environment for a Google App.

An instance of the user-interface environment for a Google App that allows the script to add features like menus, dialogs, and sidebars. A script can only interact with the UI for the current instance of an open editor, and only if the script is container-bound to the editor.

## Methods

### alert(prompt: String) → Button

Opens a dialog box in the user's editor with the given message and an "OK" button. This method suspends the server-side script while the dialog is open. The script resumes after the user dismisses the dialog, but Jdbc connections and LockService locks don't persist across the suspension.

**Parameters:**
- `prompt` (String): The message to display in the dialog box.

### alert(prompt: String, buttons: ButtonSet) → Button

Opens a dialog box in the user's editor with the given message and set of buttons. This method suspends the server-side script while the dialog is open. The script resumes after the user dismisses the dialog, but Jdbc connections and LockService locks don't persist across the suspension.

**Parameters:**
- `prompt` (String): The message to display in the dialog box.
- `buttons` (ButtonSet): The button set to display in the dialog box.

### alert(title: String, prompt: String, buttons: ButtonSet) → Button

Opens a dialog box in the user's editor with the given title, message, and set of buttons.

**Parameters:**
- `title` (String): The title to display above the dialog box.
- `prompt` (String): The message to display in the dialog box.
- `buttons` (ButtonSet): The button set to display in the dialog box.

### createAddonMenu() → Menu

Creates a builder that can be used to insert a sub-menu into the editor's Extensions menu. The menu isn't actually be updated until `Menu.addToUi()` is called.

### createMenu(caption: String) → Menu

Creates a builder that can be used to add a menu to the editor's user interface. The menu isn't actually be added until `Menu.addToUi()` is called.

**Parameters:**
- `caption` (String): The label for the menu, with all major words capitalized for a top-level menu, or only the first word capitalized for a sub-menu.

### prompt(prompt: String) → PromptResponse

Opens an input dialog box in the user's editor with the given message and an "OK" button. This method suspends the server-side script while the dialog is open.

**Parameters:**
- `prompt` (String): The message to display in the dialog box.

### prompt(prompt: String, buttons: ButtonSet) → PromptResponse

Opens an input dialog box in the user's editor with the given message and set of buttons.

**Parameters:**
- `prompt` (String): The message to display in the dialog box.
- `buttons` (ButtonSet): The button set to display in the dialog box.

### prompt(title: String, prompt: String, buttons: ButtonSet) → PromptResponse

Opens an input dialog box in the user's editor with the given title, message, and set of buttons.

**Parameters:**
- `title` (String): The title to display above the dialog box.
- `prompt` (String): The message to display in the dialog box.
- `buttons` (ButtonSet): The button set to display in the dialog box.

### showModalDialog(userInterface: Object, title: String) → void

Opens a modal dialog box in the user's editor with custom client-side content. This method does not suspend the server-side script while the dialog is open.

**Parameters:**
- `userInterface` (Object): An HtmlOutput representing the interface to display.
- `title` (String): The title of the dialog; overrides any title set by calling `setTitle()` on the userInterface object.

### showModelessDialog(userInterface: Object, title: String) → void

Opens a modeless dialog box in the user's editor with custom client-side content. This method does not suspend the server-side script while the dialog is open.

**Parameters:**
- `userInterface` (Object): An HtmlOutput representing the interface to display.
- `title` (String): The title of the dialog; overrides any title set by calling `setTitle()` on the userInterface object.

### showSidebar(userInterface: Object) → void

Opens a sidebar in the user's editor with custom client-side content. This method does not suspend the server-side script while the sidebar is open.

**Parameters:**
- `userInterface` (Object): An HtmlOutput representing the interface to display.

## Deprecated Methods

### showDialog(userInterface: Object) → void

Deprecated as of March 2014. Use `showModelessDialog()` or preferably `showModalDialog()` instead.

**Parameters:**
- `userInterface` (Object): An HtmlOutput representing the interface to display.

## Properties

| Property | Type | Description |
|----------|------|-------------|
| `Button` | `Button` | An enum representing predetermined, localized dialog buttons returned by an `alert()` or `PromptResponse.getSelectedButton()` to indicate which button in a dialog the user clicked. |
| `ButtonSet` | `ButtonSet` | An enum representing predetermined, localized sets of one or more dialog buttons that can be added to an `alert()` or a `prompt()`. |
