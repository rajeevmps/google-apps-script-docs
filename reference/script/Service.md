# Service

Access and manipulate script publishing.

Access and manipulate script publishing.

## Methods

### getUrl() → String

Returns the URL of the web app, if it has been deployed; otherwise returns `null`. If you are running the development mode web app, this returns the development mode url.

**Return:** `String` — The URL of the web app.

```javascript
MailApp.sendMail(
    'myself@example.com',
    'My Snazzy App',
    `My new app is now available at ${ScriptApp.getService().getUrl()}`,
);
```

### isEnabled() → Boolean

Returns `true` if the script is accessible as a web app.

**Return:** `Boolean` — `true` if the script is published as a web app; `false` if not.

## Deprecated Methods

### disable() → void *(Deprecated)*

Disables the script from being accessed as a web app. This method is equivalent to opening the "Publish > Deploy as web app" dialog and clicking "disable web app".

```javascript
ScriptApp.getService().disable();
```
