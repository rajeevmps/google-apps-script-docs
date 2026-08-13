# Class google.script.url (Client-side API)

## Page Summary

- `google.script.url` is a client-side JavaScript API for querying URLs to get current URL parameters and fragments.
- This API works with the `google.script.history` API and is intended for web apps using `IFRAME`.
- It is not for use in sidebars or dialogs within add-ons or container-script contexts.
- The `getLocation(function)` method gets a URL location object and passes it to a specified callback function.
- The location object contains fields like `location.hash`, `location.parameter`, and `location.parameters` to access parts of the URL.

`google.script.url` is an asynchronous client-side JavaScript
 API that can query URLs to obtain the current URL parameters and fragment.
 This API supports the [`google.script.history`](https://developers.google.com/apps-script/guides/html/reference/history)
 API. It can only be used in the context of a web app that uses
 [`IFRAME`](https://developers.google.com/apps-script/reference/html/sandbox-mode#properties).
 It is not intended for use with sidebars and dialogs in an add-on or
 container-script context. For more information, see the
 [guide to using browser
 history in web apps](https://developers.google.com/apps-script/guides/web#web_apps_and_browser_history).

### Methods

| Method | Return type | Brief description |
|---|---|---|
| `getLocation(function)` | `void` | Gets a URL location object and passes it to the specified callback function. |

## Detailed documentation

### `getLocation(function)`

Gets a URL location object and passes it to the specified callback
 function (as the only argument).

**Index.html**

```html
google.script.url.getLocation(function(location) {
  console.log(location.parameters);
  console.log(location.hash);
});
```

#### Parameters

| Name | Type | Description |
|---|---|---|
| `function` | `Function` | a client-side callback function to run, using the location object as the only argument. |

#### Location object

| Fields |  |
|---|---|
| `location.hash` | The string value of URL fragment after the `#` character, or an empty string if no URL fragment is present — Example: `headingAnchor` |
| `location.parameter` | An object of key/value pairs that correspond to the URL request parameters. Only the first value will be returned for parameters that have multiple values. If no parameters are present, this will be an empty object. — Example: `{"name": "alice", "n": "1"}` |
| `location.parameters` | An object similar to `location.parameter`, but with an array of values for each key. If no parameters are present, this will be an empty object. — Example: `{"name": ["alice"], "n": ["1", "2"]}` |
