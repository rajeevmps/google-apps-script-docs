# XFrameOptionsMode

An enum representing the X-Frame-Options modes that can be used for client-side HtmlService scripts.

An enum representing the `X-Frame-Options` modes that can be used for client-side `HtmlService` scripts. These values are accessed via `HtmlService.XFrameOptionsMode` and set using `HtmlOutput.setXFrameOptionsMode(mode)`.

If a script does not set an `X-Frame-Options` mode, Apps Script uses `DEFAULT` mode as the default.

```javascript
// Serve HTML with no X-Frame-Options header (in Apps Script server-side code).
const output = HtmlService.createHtmlOutput('<b>Hello, world!</b>');
output.setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL);
```

## Properties

### ALLOWALL

No `X-Frame-Options` header is set. This lets any site iframe the page, so the developer should implement their own protection against clickjacking.

### DEFAULT

Sets the default value for the `X-Frame-Options` header, which preserves normal security assumptions. If a script does not set an `X-Frame-Options` mode, Apps Script uses this mode as the default.
