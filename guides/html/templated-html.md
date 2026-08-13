# HTML Service: Templated HTML

## Page Summary

- Apps Script allows mixing code and HTML for dynamic pages using scriptlets, similar to templating languages like PHP or JSP.
- Scriptlets are special tags within Apps Script templates that execute code on the server before the page is served to the user.
- There are three types of scriptlets: standard (`<? ... ?>`) for executing code, printing (`<?= ... ?>`) for outputting results with contextual escaping, and force-printing (`<?!= ... ?>`) for outputting without escaping.
- Apps Script templates can access Apps Script data by calling functions, using Apps Script APIs directly, or pushing variables to the template object.
- Debugging templates can be done by examining the server-generated code using `getCode()` or `getCodeWithComments()` methods of the `HtmlTemplate` class.

You can use templates to mix Google Apps Script code and HTML to
build dynamic pages with minimal effort. If you've used templating
languages that mix code and HTML, such as PHP, ASP, or JSP, the syntax
should feel familiar.

## Scriptlets

Apps Script templates can contain three special tags called
scriptlets. Inside a scriptlet, you can write any code that works in a
normal Apps Script file: scriptlets can call functions defined
in other code files, reference global variables, or use any of the
Apps Script APIs. You can even define functions and variables
within scriptlets, with the caveat that they can't be called by functions
defined in code files or other templates.

If you paste the following example into the script editor, the contents of the
`<?= ... ?>` tag (a print scriptlet) appear in
italics. This code runs on the server before the page is served
to the user. Because scriptlet code executes before the page is served, it
can only run once per page. Unlike client-side JavaScript or
Apps Script functions that you call through
[`google.script.run`](https://developers.google.com/apps-script/guides/html/communication), scriptlets can't
execute again after the page loads.

**Code.gs**

```javascript
function doGet() {
  return HtmlService
      .createTemplateFromFile('Index')
      .evaluate();
}
```

**Index.html**

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    Hello, World! The time is <?= new Date() ?>.
  </body>
</html>
```

Note that the `doGet` function for templated HTML differs from the examples
for [creating and serving basic HTML](https://developers.google.com/apps-script/guides/html). The function
shown here generates an
[`HtmlTemplate`](https://developers.google.com/apps-script/reference/html/html-template) object from the HTML
file, then calls its
[`evaluate`](https://developers.google.com/apps-script/reference/html/html-template#evaluate()) method to
execute the scriptlets and convert the template into an
[`HtmlOutput`](https://developers.google.com/apps-script/reference/html/html-output) object that the script
can serve to the user.

### Standard scriptlets

Standard scriptlets, which use the syntax `<? ... ?>`, execute code without
explicitly outputting content to the page. However, as this example shows, the
*result* of the code inside a scriptlet can still affect the HTML content
outside of the scriptlet:

**Code.gs**

```javascript
function doGet() {
  return HtmlService
      .createTemplateFromFile('Index')
      .evaluate();
}
```

**Index.html**

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <? if (true) { ?>
      <p>This is always served!</p>
    <? } else  { ?>
      <p>This is never served.</p>
    <? } ?>
  </body>
</html>
```

### Print scriptlets

Printing scriptlets, which use the syntax `<?= ... ?>`, output the results of
their code into the page using contextual escaping.

Contextual escaping means that Apps Script keeps track of the
output's context on the page — inside an HTML attribute, inside a client-side
`script` tag, or anywhere else — and automatically adds escape characters [to
protect against cross-site scripting (XSS)
attacks](https://developers.google.com/closure/templates/docs/security).

In this example, the first printing scriptlet outputs a string directly; it is
followed by a standard scriptlet that sets up an array and a loop, followed by
another printing scriptlet to output the contents of the array.

**Code.gs**

```javascript
function doGet() {
  return HtmlService
      .createTemplateFromFile('Index')
      .evaluate();
}
```

**Index.html**

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <?= 'My favorite Google products:' ?>
    <? var data = ['Gmail', 'Docs', 'Android'];
      for (var i = 0; i < data.length; i++) { ?>
        <b><?= data[i] ?></b>
    <? } ?>
  </body>
</html>
```

Note that a printing scriptlet only outputs the value of its first statement;
any remaining statements behave as if they were contained in a standard
scriptlet. So, for example, the scriptlet `<?= 'Hello, world!'; 'abc' ?>` only
prints "Hello, world!"

### Force-printing scriptlets

Force-printing scriptlets, which use the syntax `<?!= ... ?>`, are like printing
scriptlets except that they avoid contextual escaping.

Contextual escaping is important if your script allows untrusted user input. By
contrast, you'll need to force-print if your scriptlet's output intentionally
contains HTML or scripts that you want to insert exactly as specified.

As a general rule, use printing scriptlets rather than force-printing scriptlets
unless you know that you need to print HTML or JavaScript unchanged.

## Apps Script code in scriptlets

Scriptlets aren't restricted to running normal JavaScript; you can also use any
of the following three techniques to give your templates access to 
Apps Script
data.

Remember, however, that because template code executes before the page is served
to the user, these techniques can only feed initial content to a page. To access
 Apps Script data from a page interactively, use the
[`google.script.run`](https://developers.google.com/apps-script/guides/html/communication) API instead.

### Call Apps Script functions from a template

Scriptlets can call any function defined in an Apps Script code
file or library. This example shows one way to pull data from a spreadsheet into
a template, then construct an HTML table from the data.

**Code.gs**

```javascript
function doGet() {
  return HtmlService
      .createTemplateFromFile('Index')
      .evaluate();
}

function getData() {
  return SpreadsheetApp
      .openById('1234567890abcdefghijklmnopqrstuvwxyz')
      .getActiveSheet()
      .getDataRange()
      .getValues();
}
```

**Index.html**

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <? var data = getData(); ?>
    <table>
      <? for (var i = 0; i < data.length; i++) { ?>
        <tr>
          <? for (var j = 0; j < data[i].length; j++) { ?>
            <td><?= data[i][j] ?></td>
          <? } ?>
        </tr>
      <? } ?>
    </table>
  </body>
</html>
```

### Call Apps Script APIs directly

You can also use Apps Script code directly in scriptlets. This
example accomplishes the same result as the previous example by loading the
data in the template itself rather than through a separate function.

**Code.gs**

```javascript
function doGet() {
  return HtmlService
      .createTemplateFromFile('Index')
      .evaluate();
}
```

**Index.html**

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <? var data = SpreadsheetApp
        .openById('1234567890abcdefghijklmnopqrstuvwxyz')
        .getActiveSheet()
        .getDataRange()
        .getValues(); ?>
    <table>
      <? for (var i = 0; i < data.length; i++) { ?>
        <tr>
          <? for (var j = 0; j < data[i].length; j++) { ?>
            <td><?= data[i][j] ?></td>
          <? } ?>
        </tr>
      <? } ?>
    </table>
  </body>
</html>
```

### Push variables to templates

Lastly, you can push variables into a template by assigning them as properties
of the [`HtmlTemplate`](https://developers.google.com/apps-script/reference/html/html-template) object. Once
again, this example accomplishes the same result as the previous examples.

**Code.gs**

```javascript
function doGet() {
  var t = HtmlService.createTemplateFromFile('Index');
  t.data = SpreadsheetApp
      .openById('1234567890abcdefghijklmnopqrstuvwxyz')
      .getActiveSheet()
      .getDataRange()
      .getValues();
  return t.evaluate();
}
```

**Index.html**

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <table>
      <? for (var i = 0; i < data.length; i++) { ?>
        <tr>
          <? for (var j = 0; j < data[i].length; j++) { ?>
            <td><?= data[i][j] ?></td>
          <? } ?>
        </tr>
      <? } ?>
    </table>
  </body>
</html>
```

## Debug templates

Templates can be challenging to debug because the code you write is not executed
directly. Instead, the server transforms your template into code, then executes
that resulting code.

If it isn't obvious how the template is interpreting your scriptlets, two
debugging methods in the
[`HtmlTemplate`](https://developers.google.com/apps-script/reference/html/html-template) class can help you
better understand what's going on.

### The getCode function

The [`getCode`](https://developers.google.com/apps-script/reference/html/html-template#getCode()) function
returns a string containing the code that the server creates from the template.
If you
[log](https://developers.google.com/apps-script/guides/support/troubleshooting#logging_custom_messages) the
code, then paste it into the script editor, you can run it and [debug
it](https://developers.google.com/apps-script/guides/support/troubleshooting#debugging) like normal
Apps Script code.

Here's the template that displays a list of Google products again,
followed by the result of `getCode`:

**Code.gs**

```javascript
function myFunction() {
  Logger.log(HtmlService
      .createTemplateFromFile('Index')
      .getCode());
}
```

**Index.html**

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <?= 'My favorite Google products:' ?>
    <? var data = ['Gmail', 'Docs', 'Android'];
      for (var i = 0; i < data.length; i++) { ?>
        <b><?= data[i] ?></b>
    <? } ?>
  </body>
</html>
```

**LOG (EVALUATED)**

```javascript
(function() { var output = HtmlService.initTemplate(); output._ =  '<!DOCTYPE html>\n';
  output._ =  '<html>\n' +
    '  <head>\n' +
    '    <base target=\"_top\">\n' +
    '  </head>\n' +
    '  <body>\n' +
    '    '; output._$ =  'My favorite Google products:' ;
  output._ =  '    ';  var data = ['Gmail', 'Docs', 'Android'];
        for (var i = 0; i < data.length; i++) { ;
  output._ =  '        <b>'; output._$ =  data[i] ; output._ =  '</b>\n';
  output._ =  '    ';  } ;
  output._ =  '  </body>\n';
  output._ =  '</html>';
  /* End of user code */
  return output.$out.append('');
})();
```

### The getCodeWithComments function

The
[`getCodeWithComments`](https://developers.google.com/apps-script/reference/html/html-template#getCodeWithComments())
function is similar to `getCode()`, but returns the evaluated code as comments
that appear side-by-side with the original template.

### Walk through evaluated code

The first thing you'll notice in either sample of evaluated code is the implicit
`output` object created by the method `HtmlService.initTemplate`. This method
is undocumented because only templates themselves need to use it. `output` is a
special [`HtmlOutput`](https://developers.google.com/apps-script/reference/html/html-output) object with two
unusually named properties, `_` and `_$`, which are shorthand for calling
[`append`](https://developers.google.com/apps-script/reference/html/html-output#append(String)) and
[`appendUntrusted`](https://developers.google.com/apps-script/reference/html/html-output#appendUntrusted(String)).

`output` has one more special property, `$out`, which refers to a regular
`HtmlOutput` object that does not possess these special properties. The template
returns that normal object at the end of the code.

Now that you understand this syntax, you can follow the rest of the code. HTML
content outside of scriptlets (like the `b` tag) is appended using `output._ =`
(without [contextual
escaping](https://developers.google.com/apps-script/guides/html/templates#printing_scriptlets)), and
scriptlets are appended as JavaScript (with or without contextual escaping,
depending on the type of scriptlet).

The evaluated code preserves line numbers from the template. If you
get an error while running evaluated code, the line corresponds to the
equivalent content in the template.

### Hierarchy of comments

Because evaluated code preserves line numbers, it is possible for comments
inside scriptlets to comment out other scriptlets and even HTML code. These
examples show a few surprising effects of comments:

```html
<? var x; // a comment ?> This sentence won't print because a comment begins
inside a scriptlet on the same line.

<? var y; // ?> <?= "This sentence won't print because a comment begins inside
a scriptlet on the same line.";
output.append("This sentence prints because it's on the next line, even though
it's in the same scriptlet.") ?>

<? doSomething(); /* ?>
This entire block is commented out,
even if you add a */ in the HTML
or in a <script> */ </script> tag,
<? until you end the comment inside a scriptlet. */ ?>
```
