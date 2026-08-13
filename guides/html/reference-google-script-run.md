# Class google.script.run (Client-side API)

## Page Summary

- `google.script.run` is a client-side JavaScript API for calling server-side Apps Script functions asynchronously from HTML-service pages.
- Use `google.script.host` for interacting with dialogs or sidebars in Google Docs, Sheets, or Forms.
- The `myFunction(...)` method executes a server-side function by name, but it is asynchronous and doesn't return directly, instead passing values to success handlers.
- `withFailureHandler(function)` sets a callback to run if a server-side function throws an exception, while `withSuccessHandler(function)` sets a callback for successful function returns.
- `withUserObject(object)` allows passing a client-side object to success and failure handlers, providing context without sending the object to the server.

`google.script.run` is an asynchronous client-side JavaScript API available in
 [HTML-service pages](https://developers.google.com/apps-script/guides/html) that can call server-side Apps Script
 functions. To interact with dialogs or sidebars in Google Docs, Sheets, or Forms from client-side
 code, use [`google.script.host`](https://developers.google.com/apps-script/guides/html/reference/host). For more information, see the
 [guide to communicating with server functions](https://developers.google.com/apps-script/guides/html/communication)
 in HTML service.

### Methods

| Method | Return type | Brief description |
|---|---|---|
| `myFunction(...)` (any server-side function) | `void` | Executes the server-side Apps Script function with the corresponding name. |
| `withFailureHandler(function)` | `google.script.run` | Sets a callback function to run if the server-side function throws an exception. |
| `withSuccessHandler(function)` | `google.script.run` | Sets a callback function to run if the server-side function returns successfully. |
| `withUserObject(object)` | `google.script.run` | Sets an object to pass as a second parameter to the success and failure handlers. |

## Detailed documentation

### `myFunction(...)` (any server-side function)

Executes the server-side Apps Script function with the corresponding name.

**Code.gs**

```javascript
function doGet() {
  return HtmlService.createHtmlOutputFromFile('Index');
}

function doSomething() {
  Logger.log('I was called!');
}
```

**Index.html**

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <script>
      google.script.run.doSomething();
    </script>
  </head>
  <body>
  </body>
</html>
```

#### Parameters

| Name | Type | Description |
|---|---|---|
| `...` | Most types are legal, but not `Date` , `Function` , or DOM element besides `form` ; see description | Legal parameters are JavaScript primitives like a `Number` , `Boolean` , `String` , or `null` , as well as JavaScript objects and arrays that are composed of primitives, objects, and arrays. A `form` element within the page is also legal as a parameter, but it must be the function’s only parameter. Requests fail if you attempt to pass a `Date` , `Function` , DOM element besides a `form` , or other prohibited type, including prohibited types inside objects or arrays. Objects that create circular references will also fail, and undefined fields within arrays become `null` . Note that an object passed to the server becomes a copy of the original. If a server function receives an object and changes its properties, the properties on the client are not affected. |

#### Return

`void` — this method is asynchronous and does not return directly; however, the
 server-side function can return a value to the client as a parameter passed to a
 success handler; also, return types are subject to the
 same restrictions as parameter types, except that a `form` element is not a legal
 return type

### `withFailureHandler(function)`

Sets a callback function to run if the server-side function throws an exception. The
 `Error`
 object is passed to the function as the first argument, and the
 user object (if any) is passed as a second argument. Without
 a failure handler, failures are logged to the JavaScript console. To override this, call
 `withFailureHandler(null)` or supply a failure handler that does nothing.

**Code.gs**

```javascript
function doGet() {
  return HtmlService.createHtmlOutputFromFile('Index');
}

function getUnreadEmails() {
  // 'got' instead of 'get' will throw an error.
  return GmailApp.gotInboxUnreadCount();
}
```

**Index.html**

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <script>
      function onFailure(error) {
        var div = document.getElementById('output');
        div.innerHTML = "ERROR: " + error.message;
      }

      google.script.run.withFailureHandler(onFailure)
          .getUnreadEmails();
    </script>
  </head>
  <body>
    <div id="output"></div>
  </body>
</html>
```

#### Parameters

| Name | Type | Description |
|---|---|---|
| `function` | `Function` | a client-side callback function to run if the server-side function throws an exception; the `Error` object is passed to the function as the first argument, and the user object (if any) is passed as a second argument |

#### Return

`google.script.run` — this "script runner," for chaining

### `withSuccessHandler(function)`

Sets a callback function to run if the server-side function returns successfully. The server's
 return value is passed to the function as the first argument, and the
 user object (if any) is passed as a second argument.

**Code.gs**

```javascript
function doGet() {
  return HtmlService.createHtmlOutputFromFile('Index');
}

function getUnreadEmails() {
  return GmailApp.getInboxUnreadCount();
}
```

**Index.html**

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <script>
      function onSuccess(numUnread) {
        var div = document.getElementById('output');
        div.innerHTML = 'You have ' + numUnread
            + ' unread messages in your Gmail inbox.';
      }

      google.script.run.withSuccessHandler(onSuccess)
          .getUnreadEmails();
    </script>
  </head>
  <body>
    <div id="output"></div>
  </body>
</html>
```

#### Parameters

| Name | Type | Description |
|---|---|---|
| `function` | `Function` | a client-side callback function to run if the server-side function returns successfully; the server's return value is passed to the function as the first argument, and the user object (if any) is passed as a second argument |

#### Return

`google.script.run` — this "script runner," for chaining

### `withUserObject(object)`

Sets an object to pass as a second parameter to the success and failure handlers. This "user
 object" — not to be confused with the
 `User` class — lets the callback
 functions respond to the context in which the client contacted the server. Because user objects
 are not sent to the server, they are not subject to the restrictions on parameters and return
 values for server calls. User objects cannot, however, be objects
 constructed with the `new` operator.

**Code.gs**

```javascript
function doGet() {
  return HtmlService.createHtmlOutputFromFile('Index');
}

function getEmail() {
  return Session.getActiveUser().getEmail();
}
```

**Index.html**

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <script>
      function updateButton(email, button) {
        button.value = 'Clicked by ' + email;
      }
    </script>
  </head>
  <body>
    <input type="button" value="Not Clicked"
      onclick="google.script.run
          .withSuccessHandler(updateButton)
          .withUserObject(this)
          .getEmail()" />
  </body>
</html>
```

#### Parameters

| Name | Type | Description |
|---|---|---|
| `object` | `Object` | an object to pass as a second parameter to the success and failure handlers; because user objects are not sent to the server, they are not subject to the restrictions on parameters and return values for server calls . User objects cannot, however, be objects constructed with the `new` operator |

#### Return

`google.script.run` — this "script runner," for chaining
