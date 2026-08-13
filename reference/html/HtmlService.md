# HtmlService

Service for returning HTML and other text content from a script.

Service for returning HTML and other text content from a script. Due to security considerations, scripts cannot directly return content to a browser. Instead, they must sanitize the HTML so that it cannot perform malicious actions.

## Methods

### createHtmlOutput()

Returns: `HtmlOutput`

Creates a new `HtmlOutput` object that can be returned from the script.

```javascript
const output = HtmlService.createHtmlOutput();
```

### createHtmlOutput(blob)

Parameters:
- `blob` (`BlobSource`): the data to use for the new object

Returns: `HtmlOutput`

Creates a new `HtmlOutput` object from a `BlobSource` resource.

```javascript
function createFromBlob(blob) {
  const output = HtmlService.createHtmlOutput(blob);
  return output;
}
```

Throws: Error if the blob doesn't contain HTML or the HTML is malformed

### createHtmlOutput(html)

Parameters:
- `html` (`String`): the input content

Returns: `HtmlOutput`

Creates a new `HtmlOutput` object that can be returned from the script.

```javascript
const output = HtmlService.createHtmlOutput('<b>Hello world!</b>');
```

Throws: Error if the html is malformed

### createHtmlOutputFromFile(filename)

Parameters:
- `filename` (`String`): the name of the file to use

Returns: `HtmlOutput`

Creates a new `HtmlOutput` object from a file in the code editor.

```javascript
const output = HtmlService.createHtmlOutputFromFile('myPage');
```

Throws: Error if the file wasn't found or the HTML in it is malformed

### createTemplate(blob)

Parameters:
- `blob` (`BlobSource`): the data to use for the new object

Returns: `HtmlTemplate`

Creates a new `HtmlTemplate` object from a `BlobSource` resource.

```javascript
function createFromBlob(blob) {
  const template = HtmlService.createTemplate(blob);
  const output = template.evaluate();
  return output;
}
```

Throws: Error if the blob doesn't contain HTML

### createTemplate(html)

Parameters:
- `html` (`String`): the input content

Returns: `HtmlTemplate`

Creates a new `HtmlTemplate` object that can be returned from the script.

```javascript
const template = HtmlService.createTemplate(
    '<b>The time is &lt;?= new Date() ?&gt;</b>',
);
```

### createTemplateFromFile(filename)

Parameters:
- `filename` (`String`): the name of the file to use

Returns: `HtmlTemplate`

Creates a new `HtmlTemplate` object from a file in the code editor.

```javascript
const template = HtmlService.createTemplateFromFile('myTemplate');
```

Throws: Error if the file wasn't found

### getUserAgent()

Returns: `String`

Gets the user-agent string for the current browser. Returns `null` for most script executions if not used in a web app's `doGet()` or `doPost()` function.

## Properties

| Property | Type | Description |
|----------|------|-------------|
| `SandboxMode` | `SandboxMode` | An enum representing the sandbox modes that can be used for client-side `HtmlService` scripts. |
| `XFrameOptionsMode` | `XFrameOptionsMode` | An enum representing the `X-Frame-Options` modes that can be used for client-side `HtmlService` scripts. |
