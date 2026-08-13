# ContentService

Service for returning text content from a script.

Service for returning text content from a script. You can serve up text in various forms. For example, publish this script as a web app. Scripts cannot directly return content to a browser due to security considerations; they must serve content from a different URL.

## Methods

### createTextOutput()

Returns: `TextOutput`

Create a new TextOutput object.

```javascript
function doGet() {
  const output = ContentService.createTextOutput();
  output.append('Hello world!');
  return output;
}
```

### createTextOutput(content)

Returns: `TextOutput`

Create a new TextOutput object that can serve the given content.

**Parameters**

| Name | Type | Description |
|---|---|---|
| content | String | the content to serve. |

```javascript
function doGet() {
  const output = ContentService.createTextOutput('Hello world!');
  return output;
}
```

## Properties

| Property | Type | Description |
|---|---|---|
| MimeType | [MimeType](MimeType.md) | An enum representing the MIME types that can be served from Content Service. |
