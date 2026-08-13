# HtmlOutput

An object that can be served from a script.

An `HtmlOutput` object that can be served from a script. Due to security considerations, scripts cannot directly return HTML to a browser. Instead, they must sanitize it so that it cannot perform malicious actions. The code in HtmlOutput can include embedded JavaScript and CSS (client-side), with all content sandboxed using iframe sandboxing for security.

```javascript
function doGet() {
  return HtmlService.createHtmlOutput('<b>Hello, world!</b>');
}
```

## Methods

### addMetaTag(name, content)

Parameters:
- `name` (`String`): The value of the meta tag's name attribute
- `content` (`String`): The value of the meta tag's content attribute

Returns: `HtmlOutput` — This output, for chaining

Adds a meta tag to the page. Only specific meta tags are permitted: apple-mobile-web-app-capable, google-site-verification, mobile-web-app-capable, and viewport.

```javascript
const output = HtmlService.createHtmlOutput('<b>Hello, world!</b>');
output.addMetaTag('viewport', 'width=device-width, initial-scale=1');
```

### append(addedContent)

Parameters:
- `addedContent` (`String`): The content to append

Returns: `HtmlOutput` — This output, for chaining

Appends new content to the content of this `HtmlOutput`. Use this only for content from a trusted source, because it is not escaped.

```javascript
const output = HtmlService.createHtmlOutput('<b>Hello, world!</b>');
output.append('<p>Hello again, world.</p>');
Logger.log(output.getContent());
```

Throws: Error if the HTML is malformed

### appendUntrusted(addedContent)

Parameters:
- `addedContent` (`String`): The content to append

Returns: `HtmlOutput` — This output, for chaining

Appends new content to the content of this `HtmlOutput`, using contextual escaping. This method correctly escapes content based on the current state of the `HtmlOutput`, so that the result is a safe string with no markup or side affects.

```javascript
const output = HtmlService.createHtmlOutput('<b>Hello, world!</b>');
output.appendUntrusted('<p>Hello again, world.</p>');
Logger.log(output.getContent());
```

Throws: Error if the HTML is very malformed

### asTemplate()

Returns: `HtmlTemplate` — The new HtmlTemplate

Returns an `HtmlTemplate` backed by this `HtmlOutput`. This method enables incremental template construction, with future changes to `HtmlOutput` affecting the template contents. This method can be used to build up a template incrementally.

```javascript
const output = HtmlService.createHtmlOutput('<b>Hello, world!</b>');
const template = output.asTemplate();
```

### clear()

Returns: `HtmlOutput` — This output, for chaining

Clears the current content.

```javascript
const output = HtmlService.createHtmlOutput('<b>Hello, world!</b>');
output.clear();
```

### getAs(contentType)

Parameters:
- `contentType` (`String`): The MIME type to convert to

Returns: `Blob` — The data as a blob

Converts data inside this object to a blob in the specified content type, adding appropriate file extensions. Assumes filename portions after the final period are existing extensions to be replaced. For most blobs, 'application/pdf' is valid; for images, BMP, GIF, JPEG, PNG formats are valid.

### getBlob()

Returns: `Blob` — The data as a blob

Return the data inside this object as a blob.

### getContent()

Returns: `String` — The content that is served

Gets the content of this `HtmlOutput`.

### getFaviconUrl()

Returns: `String` — The URL of the favicon image

Gets the URL for a favicon link tag added to the page by calling `setFaviconUrl(iconUrl)`. Favicon link tags included directly in an Apps Script HTML file are ignored.

```javascript
const output = HtmlService.createHtmlOutput('<b>Hello, world!</b>');
output.setFaviconUrl('http://www.example.com/image.png');
Logger.log(output.getFaviconUrl());
```

### getHeight()

Returns: `Integer` — The height, in pixels

Gets the initial height of the custom dialog in Google Docs, Sheets, or Forms. Returns null if published as a web app. To resize an already-open dialog, use client-side code.

```javascript
const output = HtmlService.createHtmlOutput('<b>Hello, world!</b>');
output.setHeight(200);
Logger.log(output.getHeight());
```

### getMetaTags()

Returns: `HtmlOutputMetaTag[]` — An array of objects representing meta tags added to the page

Gets an array of objects that represent meta tags added to the page, as added by calling `addMetaTag(name, content)`. Meta tags included directly in an Apps Script HTML file are ignored.

```javascript
const output = HtmlService.createHtmlOutput('<b>Hello, world!</b>');
output.addMetaTag('viewport', 'width=device-width, initial-scale=1');
const tags = output.getMetaTags();
Logger.log('<meta name="%s" content="%s"/>', tags[0].getName(), tags[0].getContent());
```

### getTitle()

Returns: `String` — The title of the page

Gets the title of the output page. The HTML title element is ignored.

### getWidth()

Returns: `Integer` — The width in pixels

Gets the initial width of the custom dialog in Google Docs, Sheets, or Forms. Returns null if published as a web app. To resize an already-open dialog, use client-side code.

```javascript
const output = HtmlService.createHtmlOutput('<b>Hello, world!</b>');
output.setWidth(200);
```

### setContent(content)

Parameters:
- `content` (`String`): The content to serve

Returns: `HtmlOutput` — This output, for chaining

Sets the content of this `HtmlOutput`.

```javascript
const output = HtmlService.createHtmlOutput();
output.setContent('<b>Hello, world!</b>');
```

Throws: Error if the HTML is malformed

### setFaviconUrl(iconUrl)

Parameters:
- `iconUrl` (`String`): The URL of the favicon image, with the image extension indicating the image type

Returns: `HtmlOutput` — This output, for chaining

Adds a link tag for a favicon to the page. Favicon link tags included directly in an Apps Script HTML file are ignored.

### setHeight(height)

Parameters:
- `height` (`Integer`): The new height in pixels; null results in a default value

Returns: `HtmlOutput` — This output, for chaining

Sets the initial height of the custom dialog in Google Docs, Sheets, or Forms. Has no effect if published as a web app. To resize an already-open dialog, use client-side code.

### setSandboxMode(mode)

Parameters:
- `mode` (`SandboxMode`): The sandbox mode to use

Returns: `HtmlOutput` — This output, for chaining

This method now has no effect — previously it set the sandbox mode used for client-side scripts. All scripts now use `IFRAME` mode regardless of setting. The sandbox mode can be read client-side via `google.script.sandbox.mode`.

### setTitle(title)

Parameters:
- `title` (`String`): The new title

Returns: `HtmlOutput` — This output, for chaining

Sets the title of the output page. For web apps, this is the title of the entire page, while for `HtmlOutput` shown in Google Sheets, this is the dialog title.

```javascript
const output = HtmlService.createHtmlOutput('<b>Hello, world!</b>');
output.setTitle('My First Page');
```

### setWidth(width)

Parameters:
- `width` (`Integer`): The new width in pixels; null results in a default value

Returns: `HtmlOutput` — This output, for chaining

Sets the initial width of a custom dialog in Google Docs, Sheets, or Forms. Has no effect if published as a web app. For resizing open dialogs, use client-side code.

### setXFrameOptionsMode(mode)

Parameters:
- `mode` (`XFrameOptionsMode`): The XFrame options mode to set

Returns: `HtmlOutput` — This output, for chaining

Sets the state of the page's `X-Frame-Options` header, which controls clickjacking prevention. Setting `ALLOWALL` lets any site iframe the page, so the developer should implement their own protection against clickjacking. If a script does not set an `X-Frame-Options` mode, Apps Script uses `DEFAULT` mode as the default.

```javascript
const output = HtmlService.createHtmlOutput('<b>Hello, world!</b>');
output.setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL);
```

## Properties

None.
