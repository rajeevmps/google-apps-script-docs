# UrlFetchApp

Fetch resources and communicate with other hosts over the Internet.

Fetch resources and communicate with other hosts over the Internet. This service allows scripts to communicate with other applications or access other resources on the web by fetching URLs.

A script can use the URL Fetch service to issue HTTP and HTTPS requests and receive responses. The URL Fetch service uses Google's network infrastructure for efficiency and scaling purposes.

Requests made using this service originate from a set pool of IP ranges. You can look up the full list of IP addresses if you need to allowlist or approve these requests.

This service requires the `https://www.googleapis.com/auth/script.external_request` scope.

## Methods

### fetch(url: String) → HTTPResponse

Makes a request to fetch a URL. This works over HTTP as well as HTTPS.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| `url` | String | The URL to fetch. The URL can have up to 2,082 characters. |

**Returns:** `HTTPResponse` — The HTTP response data.

```javascript
const response = UrlFetchApp.fetch('http://www.google.com/');
Logger.log(response.getContentText());
```

### fetch(url: String, params: Object) → HTTPResponse

Makes a request to fetch a URL using optional advanced parameters. This works over HTTP as well as HTTPS.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| `url` | String | The URL to fetch. The URL can have up to 2,082 characters. |
| `params` | Object | The optional JavaScript object specifying advanced parameters |

**Advanced parameters**

The `params` object can include the following fields:

| Name | Type | Description |
|------|------|-------------|
| `contentType` | String | the content type (defaults to 'application/x-www-form-urlencoded'). Another example of content type is 'application/xml; charset=utf-8'. |
| `headers` | Object | a JavaScript key/value map of HTTP headers for the request |
| `method` | String | the HTTP method for the request: `get`, `delete`, `patch`, `post`, or `put`. The default is `get`. |
| `payload` | String | the payload (that is, the POST body) for the request. Certain HTTP methods (for example, GET) do not accept a payload. It can be a string, a byte array, a blob, or a JavaScript object. A JavaScript object is interpreted as a map of form field names to values, where the values can be either strings or blobs. |
| `useIntranet` | Boolean | Deprecated. This instructs fetch to resolve the specified URL within the intranet linked to your domain through (deprecated) SDC |
| `validateHttpsCertificates` | Boolean | If `false` the fetch ignores any invalid certificates for HTTPS requests. The default is `true`. |
| `followRedirects` | Boolean | If `false` the fetch doesn't automatically follow HTTP redirects; it returns the original HTTP response. The default is `true`. |
| `muteHttpExceptions` | Boolean | If `true` the fetch doesn't throw an exception if the response code indicates failure, and instead returns the `HTTPResponse`. The default is `false`. |
| `escaping` | Boolean | If `false` reserved characters in the URL aren't escaped. The default is `true`. |
| `timeoutSeconds` | Integer | The maximum time in seconds to wait for the request to complete. The default is `360` (6 minutes). |

**Returns:** `HTTPResponse` — The HTTP response data.

```javascript
const response = UrlFetchApp.fetch('http://www.google.com/');
Logger.log(response.getContentText());

const resumeBlob = Utilities.newBlob('Hire me!', 'text/plain', 'resume.txt');
const formData = {
  name: 'Bob Smith',
  email: 'bob@example.com',
  resume: resumeBlob,
};
const options = {
  method: 'post',
  payload: formData,
};
UrlFetchApp.fetch('https://httpbin.org/post', options);

const data = {
  name: 'Bob Smith',
  age: 35,
  pets: ['fido', 'fluffy'],
};
const options = {
  method: 'post',
  contentType: 'application/json',
  payload: JSON.stringify(data),
};
UrlFetchApp.fetch('https://httpbin.org/post', options);
```

### fetchAll(requests: Object[]) → HTTPResponse[]

Makes multiple requests to fetch multiple URLs using optional advanced parameters. This works over HTTP as well as HTTPS.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| `requests` | Object[] | An array of either URLs or JavaScript objects specifying requests |

**Advanced parameters (per request object)**

Each object in the `requests` array can include the following fields:

| Name | Type | Description |
|------|------|-------------|
| `url` | String | the URL to fetch. The URL can have up to 2,082 characters. |
| `contentType` | String | the content type (defaults to 'application/x-www-form-urlencoded'). Another example of content type is 'application/xml; charset=utf-8'. |
| `headers` | Object | a JavaScript key/value map of HTTP headers for the request |
| `method` | String | the HTTP method for the request: `get`, `delete`, `patch`, `post`, or `put`. The default is `get`. |
| `payload` | String | the payload (that is, the POST body) for the request. Certain HTTP methods (for example, GET) do not accept a payload. It can be a string, a byte array, a blob, or a JavaScript object. A JavaScript object is interpreted as a map of form field names to values, where the values can be either strings or blobs. |
| `useIntranet` | Boolean | Deprecated. This instructs fetch to resolve the specified URL within the intranet linked to your domain through (deprecated) SDC |
| `validateHttpsCertificates` | Boolean | If `false` the fetch ignores any invalid certificates for HTTPS requests. The default is `true`. |
| `followRedirects` | Boolean | If `false` the fetch doesn't automatically follow HTTP redirects; it returns the original HTTP response. The default is `true`. |
| `muteHttpExceptions` | Boolean | If `true`, the fetch doesn't throw an exception if the response code indicates failure, and instead returns the `HTTPResponse`. The default is `false`. |
| `escaping` | Boolean | If `false`, reserved characters in the URL are not escaped. The default is `true`. |
| `timeoutSeconds` | Integer | The maximum time in seconds to wait for the request to complete. The default is `360` (6 minutes). |

**Returns:** `HTTPResponse[]` — An array of HTTP response data from each input request.

```javascript
const resumeBlob = Utilities.newBlob('Hire me!', 'text/plain', 'resume.txt');
const formData = {
  name: 'Bob Smith',
  email: 'bob@example.com',
  resume: resumeBlob,
};
const request1 = {
  url: 'https://httpbin.org/post',
  method: 'post',
  payload: formData,
};
const request2 = 'https://httpbin.org/get?key=value';
UrlFetchApp.fetchAll([request1, request2]);
```

### getRequest(url: String) → Object

Returns the request that is made if the operation was invoked. This method does not actually issue the request.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| `url` | String | The URL to look up. The URL can have up to 2,082 characters. |

**Returns:** `Object` — A map of Field Name to Value. The map has at least the following keys: `url`, `method`, `contentType`, `payload`, and `headers`.

```javascript
const response = UrlFetchApp.getRequest('http://www.google.com/');
for (const i in response) {
  Logger.log(`${i}: ${response[i]}`);
}
```

### getRequest(url: String, params: Object) → Object

Returns the request that is made if the operation were invoked. This method does not actually issue the request.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| `url` | String | The URL to look up. The URL can have up to 2,082 characters. |
| `params` | Object | An optional JavaScript object specifying advanced parameters |

**Advanced parameters**

The `params` object can include the following fields:

| Name | Type | Description |
|------|------|-------------|
| `contentType` | String | the content type (defaults to 'application/x-www-form-urlencoded'). Another example of content type is 'application/xml; charset=utf-8'. |
| `headers` | Object | a JavaScript key/value map of HTTP headers for the request |
| `method` | String | the HTTP method for the request: `get`, `delete`, `patch`, `post`, or `put`. The default is `get`. |
| `payload` | String | the payload (that is, the POST body) for the request. Certain HTTP methods (for example, GET) do not accept a payload. It can be a string, a byte array, a blob, or a JavaScript object. A JavaScript object is interpreted as a map of form field names to values, where the values can be either strings or blobs. |
| `useIntranet` | Boolean | Deprecated. This instructs fetch to resolve the specified URL within the intranet linked to your domain through (deprecated) SDC |
| `validateHttpsCertificates` | Boolean | If `false` the fetch ignores any invalid certificates for HTTPS requests. The default is `true`. |
| `followRedirects` | Boolean | If `false` the fetch doesn't automatically follow HTTP redirects; it returns the original HTTP response. The default is `true`. |
| `muteHttpExceptions` | Boolean | If `true` the fetch doesn't throw an exception if the response code indicates failure, and instead returns the `HTTPResponse`. The default is `false`. |
| `escaping` | Boolean | If `false` reserved characters in the URL aren't be escaped. The default is `true`. |

**Returns:** `Object` — A map of Field Name to Value. The map has at least the following keys: `url`, `method`, `contentType`, `payload`, and `headers`.

## Properties

No properties are listed for this class.
