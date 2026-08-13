# Migrate to IFRAME Sandbox Mode

## Page Summary

- All Apps Script sandbox modes except `IFRAME` are sunset, and apps using older modes now automatically use `IFRAME` mode.
- Apps migrating to `IFRAME` mode may need to set the link target attribute, include top-level HTML tags, explicitly load the `api.js` library, call `setOrigin()` for Google Picker, note potential lack of support on older browsers, use HTTPS for imported resources, and prevent default form submissions.
- Setting the link target attribute to `_top` or `_blank` is required in `IFRAME` mode and can be done via the link tag or a `<base>` tag.
- HTML files must include `<!DOCTYPE html>`, `<html>`, and `<body>` tags in `IFRAME` mode.
- The Google native loader library `api.js` must now be explicitly loaded using a script tag.
- Users of the Google Picker API need to call `setOrigin()` with `google.script.host.origin`.
- `IFRAME` mode, based on HTML5 iframe sandboxing, is not supported in some older browsers like IE9.
- Resources imported into apps must now use HTTPS instead of HTTP.
- Form submissions are no longer prevented by default in `IFRAME` mode, requiring JavaScript to prevent default behavior for click handlers to function.

Google Apps Script uses a [security sandbox](https://developers.google.com/apps-script/guides/html/restrictions)
to provide protective isolation for Google Workspace applications in
certain situations. All sandbox modes are now sunset except for `IFRAME`. Apps
using older sandbox modes now use the newer `IFRAME` mode automatically.

Apps that previously used these older modes with the HTML Service may need to
make changes for `IFRAME` mode, to address the following differences:

- You now must override the link's `target` attribute using `target="_top"` or
`target="_blank"`
- HTML files served by the HTML Service must include
<!DOCTYPE html>, <html>, and <body> tags
- The `gapi` loader library (`api.js`) doesn't load automatically in
`IFRAME` mode
- [Picker](https://developers.google.com/apps-script/guides/dialogs#file-open_dialogs) users need to call
`setOrigin` because content is served from a new domain
- Some older browsers, including IE9, are not supported
- Imported resources must now use HTTPS
- Form submission are no longer prevented by default

These differences are detailed in the following sections.

## Set the link target attribute

In the `IFRAME` mode you need to set the link target attribute to either `_top`
or `_blank`:

**Code.js**

```javascript
function doGet() {
  var template = HtmlService.createTemplateFromFile('top');
  return template.evaluate();
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

You can also override this attribute using the <base> tag within the head
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

## Top-level HTML tags

Under `NATIVE` (and `EMULATED`) sandbox mode, certain HTML tags would be
automatically added to an Apps Script .html file, but this does
not happen when using `IFRAME` mode.

To make sure your project pages are served correctly using `IFRAME`, wrap your
page content in the following top-level tags:

```html
<!DOCTYPE html>
<html>
  <body>
    <!-- Add your HTML content here -->
  </body>
</html>
```

## The gapi loader library must be explicitly loaded

Scripts that relied on automatic loading of the `gapi` loader library (`api.js`)
must be changed to load this library explicitly, as in the following example:

```html
<script src="https://apis.google.com/js/api.js?onload=onApiLoad">
</script>
```

## Google Picker API change

When using the [Google Picker API](https://developers.google.com/apps-script/guides/dialogs#file-open_dialogs),
you must now call `setOrigin` when constructing the PickerBuilder and pass in
the origin `google.script.host.origin`, as shown in the following example:

```javascript
function createPicker(oauthToken) {
  var picker = new google.picker.PickerBuilder()
      .addView(google.picker.ViewId.SPREADSHEETS) // Or a different ViewId
      .setOAuthToken(oauthToken)
      .setDeveloperKey(developerKey)
      .setCallback(pickerCallback)
      .setOrigin(google.script.host.origin) // Note the setOrigin
      .build();
  picker.setVisible(true);
}
```

For a full working example, see
[File-open dialogs](https://developers.google.com/apps-script/guides/dialogs#file-open_dialogs).

## Browser support

The `IFRAME` sandbox mode is based on the
[iframe sandboxing](http://caniuse.com/#search=sandbox) feature in HTML5.
This is not supported in some older browsers, such as Internet Explorer 9. This
can be an issue if your Apps Script project both:

- uses `HtmlService`, and
- previously used `EMULATED` or `NATIVE` sandboxing

Migrating these apps to `IFRAME` sandbox mode means they may no longer work on
some older browsers (notably IE9 and earlier) that don't support HTML5's iframe
sandboxing feature.

Apps that already request `IFRAME` mode or don't use `HtmlService` at all are
unaffected by this issue.

## HTTPS is now required for imported resources

Previous applications that imported resources using HTTP must be changed to
use HTTPS instead.

## Form submission are no longer prevented by default

Under `NATIVE` sandboxing HTML forms were prevented from actually submitting
and navigating the page. Given that, a developer could add an `onclick`
handler to the submit button and not have to worry about what happened after.

With `IFRAME` mode however HTML forms are allowed to submit, and if a form
element has no `action` attribute specified it will submit to a blank page.
Worse, the inner iframe will redirect to the blank page before the `onclick`
handler has a chance to finish.

The solution is to add JavaScript code to your page that prevents the form
elements from actually submitting, so that the click handlers have time to
function:

```javascript
// Prevent forms from submitting.
function preventFormSubmit() {
  var forms = document.querySelectorAll('form');
  for (var i = 0; i < forms.length; i++) {
    forms[i].addEventListener('submit', function(event) {
      event.preventDefault();
    });
  }
}
window.addEventListener('load', preventFormSubmit);
```

A complete example can be found on the HtmlService guide
[Client-to-Server Communication](https://developers.google.com/apps-script/guides/html/communication#forms).
