# Content Service

## Page Summary

- Apps Script's Content service allows scripts to act as "services" by responding to GET and POST requests with raw textual content of various MIME types instead of a user interface.
- A simple example demonstrates returning "Hello, world!" as plain text using `ContentService.createTextOutput()`.
- The Content service can be used for more complex tasks like modifying and serving RSS feeds by fetching external data, processing it, and setting the appropriate MIME type.
- Scripts can serve JSON data to other scripts or services, as shown with an example that checks calendar availability and returns a JSON object.
- By adding a prefix parameter and setting the MIME type to JAVASCRIPT, JSON services can be transformed into JSONP to be called from JavaScript in a browser, though caution is advised due to security risks.

that return raw textual content of various MIME types.

When a script is published as a web app, the callback functions `doGet` and
`doPost` execute whenever a request is made to the script's URL. Instead of
returning a user interface object created with the
[HTML service](https://developers.google.com/apps-script/guides/html), the
[Content service](https://developers.google.com/apps-script/reference/content) can return raw textual
content. Write scripts that act as services, responding to `GET` and `POST`
requests and serving data of various MIME types.

## The basics

The following example shows how to use the Content service:

```javascript
function doGet() {
  return ContentService.createTextOutput('Hello, world!');
}
```

[Deploy the script as a web app](https://developers.google.com/apps-script/guides/web#deploying_a_script_as_a_web_app).
Follow the same steps as serving a user interface. When a `GET` request is made
to the script's URL, the text `Hello, world!` returns. In addition to plain
text, the service supports returning ATOM, CSV, iCal, JavaScript, JSON, RSS,
vCard, and XML content.

## Serve RSS feeds

Filter an RSS feed to modify its content. For example, edit an
[XKCD](http://xkcd.com/) feed to include alt text directly in the feed for
better mobile viewing.

```javascript
function doGet() {
  var feed = UrlFetchApp.fetch('http://xkcd.com/rss.xml').getContentText();
  feed = feed.replace(
    /(&lt;img.*?alt="(.*?)".*?&gt;)/g,
    '$1' + new Array(10).join('&lt;br /&gt;') + '$2');
  return ContentService.createTextOutput(feed)
    .setMimeType(ContentService.MimeType.RSS);
}
```

The code consists of the following components. Use the
[URL Fetch service](https://developers.google.com/apps-script/reference/url-fetch) to fetch the original
XKCD RSS feed. Use a standard JavaScript regular expression to make the
substitutions. Wrap the edited feed in a
[TextOutput](https://developers.google.com/apps-script/reference/content/text-output) object and set the MIME
type to RSS.

To see this in action, publish the script as a web app and allow anonymous
access. Add the URL of the service to your RSS reader or visit it directly in a
web browser.

## Serve JSON from scripts

Use the Content service to serve JSON to other scripts, websites, and services.
The following script implements a service that checks if a calendar slot is
open at a specific time.

```javascript
function doGet(request) {
  var events = CalendarApp.getEvents(
    new Date(Number(request.parameters.start) * 1000),
    new Date(Number(request.parameters.end) * 1000));
  var result = {
    available: events.length == 0
  };
  return ContentService.createTextOutput(JSON.stringify(result))
    .setMimeType(ContentService.MimeType.JSON);
}
```

Publish this as an anonymous web app. Users can add URL parameters to the end
of the service URL. The `start` and `end` parameters specify a time range in
the standard Unix epoch.

```bash session
curl -L URL_OF_YOUR_SCRIPT?start=1325437200&end=1325439000
```

The service returns JSON that reports if the calendar is open in that range.

```json
{"available":true}
```

## Serve JSONP in web pages

With a slight change, your JSON service can become
[JSONP](http://en.wikipedia.org/wiki/JSONP) to be called from JavaScript in a
browser.

```javascript
function doGet(request) {
  var events = CalendarApp.getEvents(
    new Date(Number(request.parameters.start) * 1000),
    new Date(Number(request.parameters.end) * 1000));
  var result = {
    available: events.length == 0
  };
  return ContentService.createTextOutput(
    request.parameters.prefix + '(' + JSON.stringify(result) + ')')
    .setMimeType(ContentService.MimeType.JAVASCRIPT);
}
```

To call this service from a browser, create a script tag with a `src` attribute
set to the service URL and an additional `prefix` parameter. This is the name
of the function in your client-side JavaScript that is called with the value
returned by the service.

```html
<script src="URL_OF_YOUR_SCRIPT?start=1325437200&end=1325439000&prefix=alert"></script>
```

This example shows a message box in the browser with the service output, using
the browser's built-in `alert` function as the prefix. The JavaScript code
returned looks like:

```javascript
alert({"available":true})
```

Be careful when using JSONP. Because anyone can embed the script tag in their
web page, you can be tricked into executing the script when visiting a
malicious website, which can then capture returned data. Ensure JSONP scripts
are read-only and only return non-sensitive information.

## Redirects

For security, content returned by the Content service is redirected to a
one-time URL at `script.googleusercontent.com`. If you use the Content service
to return data to another application, ensure the HTTP client is configured to
follow redirects. For the curl command-line utility, add the flag `-L`. Check
the documentation for your HTTP client for more information.
