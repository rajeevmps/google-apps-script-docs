# Menu

A custom menu in an instance of the user interface for a Google App.

A custom menu in an instance of the user interface for a Google App. A script can only interact with the UI for the current instance of an open document or form, and only if the script is container-bound to the document or form.

## Methods

### addItem(caption: String, functionName: String) → Menu

Adds an item to the menu. The label for a menu item should be in sentence case (only the first word capitalized).

**Parameters:**
- `caption` (String): The label for the menu item, with only the first word capitalized.
- `functionName` (String): The name of the function to invoke when the user selects the item. You can use functions from included libraries, such as `Library.libFunction1`.

### addSeparator() → Menu

Adds a visual separator to the menu.

### addSubMenu(menu: Menu) → Menu

Adds a sub-menu to the menu.

**Parameters:**
- `menu` (Menu): The sub-menu, constructed like a top-level menu.

### addToUi() → void

Inserts the menu into the instance of the editor's user interface.

## Code Sample

```javascript
function onOpen(e) {
  SpreadsheetApp.getUi()
      .createMenu('My Menu')
      .addItem('My Menu Item', 'myFunction')
      .addSeparator()
      .addSubMenu(
          SpreadsheetApp.getUi()
              .createMenu('My Submenu')
              .addItem('One Submenu Item', 'mySecondFunction')
              .addItem('Another Submenu Item', 'myThirdFunction'),
          )
      .addToUi();
}
```
