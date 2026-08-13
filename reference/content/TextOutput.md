# TextOutput

A TextOutput object that can be served from a script.

A TextOutput object that can be served from a script. Due to security considerations, scripts cannot directly return text content to a browser. Instead, the browser is redirected to googleusercontent.com, which will display it without any further sanitization or manipulation. This class supports serving various content types, including JSON, RSS, and XML. Objects of this type are created using `ContentService.createTextOutput()`, typically from within a `doGet()` or `doPost()` function used to implement a web app.

```javascript
function doGet() {
  return ContentService.createTextOutput('hello world!');
}
```

## Methods

### append(addedContent)

Returns: `TextOutput`

Appends new content to the content that will be served. Returns the TextOutput itself, for chaining.

**Parameters**

| Name | Type | Description |
|---|---|---|
| addedContent | String | the content to append |

### clear()

Returns: `TextOutput`

Clears the current content. Returns the TextOutput itself, for chaining.

### downloadAsFile(filename)

Returns: `TextOutput`

Tells browsers to download rather than display this content. Some browsers will ignore this setting. Setting this to null will clear it back to the default behavior of displaying rather than downloading. Throws an Error if the filename contains illegal characters (such as `:`, `/`, or `\`).

**Parameters**

| Name | Type | Description |
|---|---|---|
| filename | String | the file name to use |

### getContent()

Returns: `String`

Gets the content that will be served.

### getFileName()

Returns: `String`

Returns the file name to download this file as, or null if it should be displayed rather than downloaded.

### getMimeType()

Returns: `MimeType`

Get the mime type this content will be served with.

### setContent(content)

Returns: `TextOutput`

Sets the content that will be served. Returns the TextOutput itself, for chaining.

**Parameters**

| Name | Type | Description |
|---|---|---|
| content | String | the content to serve |

### setMimeType(mimeType)

Returns: `TextOutput`

Sets the mime type for content that will be served. The default is plain text. Returns the TextOutput itself, for chaining.

**Parameters**

| Name | Type | Description |
|---|---|---|
| mimeType | MimeType | the mime type to use |

## Properties

None.
