# OverflowMenu

Holds a list of OverflowMenuItem objects that are displayed in a pop-up menu.

Holds a list of `OverflowMenuItem` objects that are displayed in a pop-up menu. Available for Google Chat apps. In developer preview for Google Workspace add-ons.

## Methods

### addMenuItem(menuItem: OverflowMenuItem): OverflowMenu

Adds a menu item.

Parameters:
- `menuItem` (OverflowMenuItem): The menu item to add.

Return: This object, for chaining.

```javascript
const overflowMenuItem = CardService.newOverflowMenuItem();
// Finish building the overflow menu item...

const overflowMenu =
    CardService.newOverflowMenu().addMenuItem(overflowMenuItem);
```
