# HTML Service: Restrictions

## Page Summary

- Apps Script uses iframes to sandbox HTML-service web apps and custom user interfaces for security.
- The only remaining sandbox mode is `IFRAME`; older modes are automatically migrated to this mode.
- The `IFRAME` sandbox mode restricts certain actions, such as top-level navigation, by using specific HTML5 iframe sandboxing attributes.
- In `IFRAME` mode, link targets must be set to `_top` or `_blank`.
- Active content in `IFRAME` mode, such as scripts and external stylesheets, must be loaded over HTTPS.

To protect users from malicious HTML or JavaScript, the HTML service uses
iframes to sandbox web apps or custom user interfaces for Google Docs,
Google Sheets, and Forms. The HTML service doesn't use a
sandbox in other situations, such as generating the body of an email. The
sandbox imposes limitations on client-side code.

## Sandbox Mode

With the exception of `IFRAME`, all sandbox modes are sunset. Apps that
previously used `NATIVE` or `EMULATED` modes now automatically use `IFRAME`
mode. If your script was developed with an older mode, follow the
[migration instructions](https://developers.google.com/apps-script/migration/iframe) to ensure it functions
properly.

The [`setSandboxMode`](https://developers.google.com/apps-script/reference/html/html-output#setSandboxMode(SandboxMode))
method now has no effect when called.

## Restrictions in IFRAME mode

The `IFRAME` sandbox mode is based on the
[iframe sandboxing](https://html.spec.whatwg.org/#attr-iframe-sandbox) feature
in HTML5, using the following keywords:

- `allow-same-origin`
- `allow-forms`
- `allow-scripts`
- `allow-popups`
- `allow-downloads`
- `allow-modals`
- `allow-popups-to-escape-sandbox`
- `allow-top-navigation-by-user-activation` - This attribute is only set for
[stand-alone script projects](https://developers.google.com/apps-script/guides/standalone).

The `allow-top-navigation` keyword, which allows the content to navigate its
top-level browsing context, is restricted and not set as an attribute in the
sandbox. If you need to redirect your script, add a link or a button for the
user to take action on instead.

### Set the link target attribute

In the `IFRAME` mode you need to set the link target attribute to either
`_top` or `_blank`:

**Code.js**

```javascript
function doGet() {
  var template = HtmlService.createTemplateFromFile('top');
  return template.evaluate().setSandboxMode(HtmlService.SandboxMode.IFRAME);
}
```

**top.html**

```html
<!DOCTYPE html>
<html>
 <body>
   <div>
     <a href="http://google.com" target="_top">Click Me!</a>
   </div>
 </body>
</html>
```

You can also override this attribute using the `<base>` tag within the head
section of the enclosing web page:

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
   <div>
     <a href="http://google.com">Click Me!</a>
   </div>
 </body>
</html>
```

### HTTPS required for active content

["Active"
content](https://developer.mozilla.org/en-US/docs/Security/MixedContent#Mixed_active_content)
like scripts, external stylesheets, and XmlHttpRequests must be loaded over
HTTPS, not HTTP.
