# Grid

A Grid is an organized grid used to display a collection of grid items. The Grid is available for Google Workspace add-ons and Google Chat apps.

Grids support methods to add items, set authorization, border, compose, click, and open link actions, define the number of columns, and set a title.

A UI object can only have one click or action method set at a time.

## Methods

### addEventAction(eventAction): Widget

Adds the event action that can be performed on the widget.

### addItem(gridItem): Grid

Adds a new grid item to the grid.

### setAuthorizationAction(action): Grid

Sets an authorization action that opens a URL to the authorization flow when the object is clicked. This opens the URL in a new window. When the user finishes the authorization flow and returns to the application, the add-on reloads.

### setBorderStyle(borderStyle): Grid

Sets the border style applied to each grid item. Default is NO_BORDER.

### setComposeAction(action, composedEmailType): Grid

Sets an action that composes a draft email when the object is clicked.

### setId(id): Widget

Sets the unique ID assigned that's used to identify the widget to be mutated. Widget mutation is only supported in Add-Ons.

### setNumColumns(numColumns): Grid

The number of columns to display in the grid. If shown in the right side panel, you can display 1-2 columns and the default value is 1. If shown in a dialog, you can display 2-3 columns and the default value is 2.

### setOnClickAction(action): Grid

Sets an action that executes when the object is clicked.

### setOnClickOpenLinkAction(action): Grid

Sets an action that opens a URL in a tab when the object is clicked. Use this function when the URL needs to be built or when you need to take other actions in addition to creating the OpenLink object.

### setOpenLink(openLink): Grid

Sets a URL to be opened when the object is clicked. Use this function when the URL is already known and only needs to be opened.

### setTitle(title): Grid

Sets the title text of the grid. The text must be a plain string with no formatting.

### setVisibility(visibility): Widget

Sets the visibility of the widget. The default value is `VISIBLE`.

```javascript
const grid = CardService.newGrid().setTitle('My Grid').setNumColumns(2).addItem(
    CardService.newGridItem().setTitle('My item'));
```
