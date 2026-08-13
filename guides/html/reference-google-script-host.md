# Class google.script.host (Client-side API)

## Page Summary

- `google.script.host` is a client-side JavaScript API for interacting with dialogs or sidebars in Google Docs, Sheets, or Forms containing HTML-service pages.
- It provides the `origin` property to set the host domain and methods like `close()`, `editor.focus()`, `setHeight()`, and `setWidth()`.
- The `close()` method is used to close the current dialog or sidebar.
- The `editor.focus()` method switches focus from the dialog or sidebar back to the Google editor.
- The `setHeight()` and `setWidth()` methods are used to adjust the dimensions of a dialog.

`google.script.host` is an asynchronous client-side JavaScript API that can interact
 with dialogs or sidebars in Google Docs, Sheets, or Forms that contain
 [HTML-service pages](https://developers.google.com/apps-script/guides/html). To execute server-side functions from
 client-side code, use [`google.script.run`](https://developers.google.com/apps-script/guides/html/reference/run). For more information, see
 the
 [guide to communicating with server functions](https://developers.google.com/apps-script/guides/html/communication)
 in HTML service.

### Properties

| Property | Description |
|---|---|
| `origin` | Provides the host domain, so scripts can set their origin correctly. |

### Methods

| Method | Return type | Brief description |
|---|---|---|
| `close()` | `void` | Closes the current dialog or sidebar. |
| `editor.focus()` | `void` | Switches browser focus from the dialog or sidebar to the Google Docs, Sheets, or Forms editor. |
| `setHeight(height)` | `void` | Sets the height of the current dialog. |
| `setWidth(width)` | `void` | Sets the width of the current dialog. |

## Detailed documentation

### `close()`

Closes the current dialog or sidebar.

**Code.gs**

```javascript
function onOpen(e) {
  SpreadsheetApp.getUi() // Or DocumentApp or FormApp.
      .createMenu('Sidebar').addItem('Show', 'showSidebar').addToUi();
}

function showSidebar() {
  var html = HtmlService.createHtmlOutputFromFile('Index');
  SpreadsheetApp.getUi() // Or DocumentApp or FormApp.
      .showSidebar(html);
}
```

**Index.html**

```html
<input type="button" value="Close"
  onclick="google.script.host.close()" />
```

### `editor.focus()`

Switches browser focus from the dialog or sidebar to the Google Docs, Sheets, or Forms editor.

**Code.gs**

```javascript
function onOpen(e) {
  SpreadsheetApp.getUi() // Or DocumentApp or FormApp.
      .createMenu('Sidebar').addItem('Show', 'showSidebar').addToUi();
}

function showSidebar() {
  var html = HtmlService.createHtmlOutputFromFile('Index');
  SpreadsheetApp.getUi() // Or DocumentApp or FormApp.
      .showSidebar(html);
}
```

**Index.html**

```html
<input type="button" value="Switch focus"
  onclick="google.script.host.editor.focus()" />
```

### `setHeight(height)`

Sets the height of the current dialog.

**Code.gs**

```javascript
function onOpen(e) {
  SpreadsheetApp.getUi() // Or DocumentApp or FormApp.
      .createMenu('Dialog').addItem('Show', 'showDialog').addToUi();
}

function showDialog() {
  var html = HtmlService.createHtmlOutputFromFile('Index')
      .setWidth(300)
      .setHeight(200);
  SpreadsheetApp.getUi() // Or DocumentApp or FormApp.
      .showModalDialog(html, 'Dialog title');
}
```

**Index.html**

```html
<script>
  function resizeDialog(width, height) {
    google.script.host.setWidth(width);
    google.script.host.setHeight(height);
  }
</script>
<input type="button" value="Resize dialog"
  onclick="resizeDialog(450, 300)" />
```

#### Parameters

| Name | Type | Description |
|---|---|---|
| `height` | `Integer` | the new height, in pixels |

### `setWidth(width)`

Sets the width of the current dialog.

**Code.gs**

```javascript
function onOpen(e) {
  SpreadsheetApp.getUi() // Or DocumentApp or FormApp.
      .createMenu('Dialog').addItem('Show', 'showDialog').addToUi();
}

function showDialog() {
  var html = HtmlService.createHtmlOutputFromFile('Index')
      .setWidth(300)
      .setHeight(200);
  SpreadsheetApp.getUi() // Or DocumentApp or FormApp.
      .showModalDialog(html, 'Dialog title');
}
```

**Index.html**

```html
<script>
  function resizeDialog(width, height) {
    google.script.host.setWidth(width);
    google.script.host.setHeight(height);
  }
</script>
<input type="button" value="Resize dialog"
  onclick="resizeDialog(450, 300)" />
```

#### Parameters

| Name | Type | Description |
|---|---|---|
| `width` | `Integer` | the new width, in pixels |
