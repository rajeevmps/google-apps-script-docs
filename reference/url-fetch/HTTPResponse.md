# HTTPResponse

This class allows users to access specific information on HTTP responses.

This class allows users to access specific information on HTTP responses.

## Methods

### getAllHeaders() → Object

Returns an attribute/value map of headers for the HTTP response, with headers that have multiple values returned as arrays.

**Returns:** `Object` — A JavaScript key/value map of HTTP headers.

```javascript
const response = UrlFetchApp.fetch('http://www.google.com/');
Logger.log(response.getAllHeaders());
```

### getAs(contentType: String) → Blob

Return the data inside this object as a blob converted to the specified content type. This method adds the appropriate extension to the filename—for example, "myfile.pdf". However, it assumes that the part of the filename that follows the last period (if any) is an existing extension that should be replaced.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| `contentType` | String | The MIME type to convert to. For most blobs, 'application/pdf' is the only valid option. For images in BMP, GIF, JPEG, or PNG format, any of 'image/bmp', 'image/gif', 'image/jpeg', or 'image/png' are also valid. For a Google Docs document, 'text/markdown' is also valid. |

**Returns:** `Blob` — The data as a blob.

### getBlob() → Blob

Return the data inside this object as a blob.

**Returns:** `Blob` — The data as a blob.

### getContent() → Byte[]

Gets the raw binary content of an HTTP response.

**Returns:** `Byte[]` — The content as a raw binary array.

```javascript
const response = UrlFetchApp.fetch('http://www.google.com/');
Logger.log(response.getContent()[0]);
```

### getContentText() → String

Gets the content of an HTTP response encoded as a string.

**Returns:** `String` — The content of the HTTP response, as a string.

```javascript
const response = UrlFetchApp.fetch('http://www.google.com/');
Logger.log(response.getContentText());
```

### getContentText(charset: String) → String

Returns the content of an HTTP response encoded as a string of the given charset.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| `charset` | String | A string representing the charset to be used for encoding the HTTP response content. |

**Returns:** `String` — The content of the HTTP response, encoded using the given charset.

```javascript
const response = UrlFetchApp.fetch('http://www.google.com/');
Logger.log(response.getContentText('UTF-8'));
```

### getHeaders() → Object

Returns an attribute/value map of headers for the HTTP response.

**Returns:** `Object` — A JavaScript key/value map of HTTP headers.

```javascript
const response = UrlFetchApp.fetch('http://www.google.com/');
Logger.log(response.getHeaders());
```

### getResponseCode() → Integer

Get the HTTP status code (200 for OK, etc.) of an HTTP response.

**Returns:** `Integer` — The HTTP response code (for example, 200 for OK).

```javascript
const response = UrlFetchApp.fetch('http://www.google.com/');
Logger.log(response.getResponseCode());
```

## Properties

No properties are listed for this class.
