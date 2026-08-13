# HTML Service: Best Practices

## Page Summary

- Separate HTML, CSS, and JavaScript into different files to improve readability and development ease.
- Load data asynchronously using `google.script.run` instead of directly in templates to ensure a responsive UI.
- Ensure external resources like JavaScript and CSS files are loaded using HTTPS to avoid mixed content errors in the `IFRAME` sandbox mode.
- Include the `<!DOCTYPE html>` declaration at the top of your HTML file to ensure modern browser rendering and avoid quirks mode.
- Load JavaScript code at the bottom of the page to allow HTML content to render first, improving responsiveness.
- Consider using the jQuery library to simplify common JavaScript tasks in web development.

Building user interfaces with the HTML service is similar to standard web
development. However, certain aspects are specific to the
Apps Script environment. This guide highlights best practices for
developing responsive and secure HTML-service UIs.

## Separate HTML, CSS, and JavaScript

Combining all HTML, CSS, and JavaScript into a single file can make projects
difficult to maintain. Although Apps Script requires client-side
code to be in .html files, you should still separate CSS and client-side
JavaScript into their own files and include them in the main HTML page with a
custom function.

The following example uses a server-side `include` function in `Code.gs` to
import `Stylesheet.html` and `JavaScript.html` into `Page.html`. When called with
[printing scriptlets](https://developers.google.com/apps-script/guides/html/templates#printing_scriptlets),
this function injects the file content directly. Because these are HTML
snippets rather than standalone .css or .js files, they must include `<style>`
and `<script>` tags.

**Code.gs**

```javascript
function doGet(request) {
  return HtmlService.createTemplateFromFile('Page')
      .evaluate();
}

function include(filename) {
  return HtmlService.createHtmlOutputFromFile(filename)
      .getContent();
}
```

**Page.html**

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <?!= include('Stylesheet'); ?>
  </head>
  <body>
    <h1>Welcome</h1>
    <p>Please enjoy this helpful script.</p>
    <?!= include('JavaScript'); ?>
  </body>
</html>
```

**Stylesheet.html**

```html
<style>
p {
  color: green;
}
</style>
```

**JavaScript.html**

```html
<script>
window.addEventListener('load', function() {
  console.log('Page is loaded');
});
</script>
```

## Load data asynchronously, not in templates

[Templated HTML](https://developers.google.com/apps-script/guides/html/templates) can be used to quickly
build interfaces, but its use should be limited to ensure your UI is
responsive. The code in templates is executed once when the page is loaded, and
no content is sent to the client until the processing is complete. Having
long-running tasks in your scriptlet code can cause your UI to appear slow.

Use scriptlet tags for quick, one-time tasks such as including other content
or setting static values. All other data should be loaded using
[`google.script.run`](https://developers.google.com/apps-script/guides/html/communication) calls.
Coding in this asynchronous manner is more difficult but allows the UI to load
more quickly and gives it the opportunity to present a spinner or other
loading message to the user.

Don't — load in templates

```html
<p>List of things:</p>
<? var things = getLotsOfThings(); ?>
<ul>
  <? for (var i = 0; i < things.length; i++) { ?>
    <li><?= things[i] ?></li>
  <? } ?>
</ul>
```

Do — load asynchronously

```html
<p>List of things:</p>
<ul id="things">
    <li>Loading...</li>
</ul>

<script
src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js">
</script>
<script>
// The code in this function runs when the page is loaded.
$(function() {
  google.script.run.withSuccessHandler(showThings)
      .getLotsOfThings();
});

function showThings(things) {
  var list = $('#things');
  list.empty();
  for (var i = 0; i < things.length; i++) {
    list.append('<li>' + things[i] + '</li>');
  }
}
</script>
```

## Load resources using HTTPS

In `IFRAME` [sandbox mode](https://developers.google.com/apps-script/guides/html/restrictions#sandbox_mode),
all JavaScript and CSS files must be served over HTTPS. Serving these files
insecurely results in errors like the following:

Mixed Content: The page at 'https://...' was loaded over HTTPS, but
requested an insecure script 'http://...'. This request has been blocked;
the content must be served over HTTPS.

Most popular libraries support both HTTP and HTTPS, so switching is usually
just a matter of inserting an addition 's' into the URL.

## Use the HTML5 document type declaration

If your page is served using the newer `IFRAME`
[sandbox mode](https://developers.google.com/apps-script/guides/html/restrictions#sandbox_mode), make sure
to include the following snippet of code at the top of your HTML file.

```html
<!DOCTYPE html>
```

This document type declaration tells the browser that you designed the page for
modern browsers, and that it shouldn't render your page using
[quirks mode](http://en.wikipedia.org/wiki/Quirks_mode). Even if you don't plan
to take advantage of modern HTML5 elements or JavaScript APIs, this helps
ensure your page is displayed correctly.

## Load JavaScript last

Many web developers recommend loading JavaScript code at the bottom of the page
to increase responsiveness, and this is even more important with the HTML
service. Moving your `<script>` tags to the end of your page lets HTML
content render before the JavaScript is processed, allowing you to present a
spinner or other message to the user.

## Take advantage of jQuery

[jQuery](http://jquery.com/) is a popular JavaScript library that simplifies
many common tasks in web development.
