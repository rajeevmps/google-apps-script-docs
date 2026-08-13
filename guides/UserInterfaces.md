# HTML Service: Create and Serve HTML

The [HTML service](https://developers.google.com/apps-script/reference/html) lets you serve web pages that
can interact with server-side Apps Script functions. It is
particularly useful for building web apps or adding custom user interfaces in
Google Docs, Google Sheets, and Forms. You can even use it to
generate the body of an email.

## Create HTML files

To add an HTML file to your Apps Script project, follow these
steps:

1. Open the Apps Script editor.
2. At the left, click Add a file \> **HTML**.

Within the HTML file, you can write most standard HTML, CSS, and client-side
JavaScript. The page is served as HTML5, although some advanced features of
HTML5 are not available, as explained in
[Restrictions](https://developers.google.com/apps-script/guides/html/restrictions).

Your file can also include template scriptlets that are processed on the server
before the page is sent to the user --- similar to PHP --- as explained in the
section on [templated HTML](https://developers.google.com/apps-script/guides/html/templates).

## Serve HTML as a web app

To create a web app with the HTML service, your code must include a `doGet`
function that tells the script how to serve the page. The function must return
an [`HtmlOutput`](https://developers.google.com/apps-script/reference/html/html-output) object, as shown in
this example.

### Code.gs

```html
function doGet() {
  return HtmlService.createHtmlOutputFromFile('Index');
}
```

### Index.html

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    Hello, World!
  </body>
</html>
```

Once that basic framework is in place, all you have to do is
[save a version of your script](https://developers.google.com/apps-script/guides/versions), then
[deploy your script as a web app](https://developers.google.com/apps-script/execution_web_apps#deploying).

After the script is deployed as a web app, you can also
[embed it in a Google Site](https://developers.google.com/apps-script/guides/web#embed_your_web_app_in).

## Serve HTML as a Google Docs, Sheets, Google Slides, or Forms user interface

The HTML service can display a [dialog or sidebar](https://developers.google.com/apps-script/guides/dialogs)
in Google Docs, Sheets, Slides, or
Forms if your script is
[container-bound](https://developers.google.com/apps-script/guides/bound) to the file. In Google Forms,
custom user interfaces are only visible to an editor who opens the form to
modify it, not to a user who opens the form to respond.

Unlike a web app, a script that creates a user interface for a document,
spreadsheet, or form does not need a `doGet` function specifically, and you
don't need to save a version of your script or deploy it. Instead, the function
that opens the user interface must pass your HTML file as an
[`HtmlOutput`](https://developers.google.com/apps-script/reference/html/html-output) object to the
`showModalDialog` or `showSidebar` methods of the
[`Ui`](https://developers.google.com/apps-script/reference/base/ui) object for the active document, form, or
spreadsheet.

These examples include a few extra features for convenience: the `onOpen`
function creates a [custom menu](https://developers.google.com/apps-script/guides/menus) that helps you
open the interface, and the button in the HTML file calls
[`google.script.host.close`](https://developers.google.com/apps-script/guides/html/reference/host#close)
to close the interface.

### Code.gs

```html
// Use this code for Google Docs, Slides, Forms, or Sheets.
function onOpen() {
  SpreadsheetApp.getUi() // Or DocumentApp or SlidesApp or FormApp.
      .createMenu('Dialog')
      .addItem('Open', 'openDialog')
      .addToUi();
}

function openDialog() {
  var html = HtmlService.createHtmlOutputFromFile('Index');
  SpreadsheetApp.getUi() // Or DocumentApp or SlidesApp or FormApp.
      .showModalDialog(html, 'Dialog title');
}
```

### Index.html

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    Hello, World!
    <input type="button" value="Close"
        onclick="google.script.host.close()" />
  </body>
</html>
```

The first time you want to display this user interface, you must
either run the `onOpen` function
[manually in the script editor](https://developers.google.com/apps-script/execution_script_editor)
or reload the window for the Docs, Sheets, or
Forms editor (which closes the
script editor). After that, the custom menu appears within a few seconds
every time you open the file. To see the interface, choose **Dialog \> Open**.

# HTML Service: Communicate with Server Functions

[`google.script.run`](https://developers.google.com/apps-script/guides/html/reference/run) is an asynchronous
client-side JavaScript API that allows HTML-service pages to call server-side
Apps Script functions. The following example shows the most basic
functionality of `google.script.run` --- [calling a function on the
server](https://developers.google.com/apps-script/guides/html/reference/run#myFunction(...)) from client-side
JavaScript.

### Code.gs

```html
function doGet() {
  return HtmlService.createHtmlOutputFromFile('Index');
}

function doSomething() {
  Logger.log('I was called!');
}
```

### Index.html

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <script>
      google.script.run.doSomething();
    </script>
  </head>
</html>
```

If you deploy this script as a web app and visit its URL, you won't see
anything, but if you view the logs, you'll see that the server function
`doSomething` was called.

Client-side calls to server-side functions are asynchronous: after the browser
requests that the server run the function `doSomething`, the browser continues
immediately to the next line of code without waiting for a response. This means
that server function calls may not execute in the order you expect. If you make
two function calls at the same time, there is no way to know which function runs
first; the result may differ each time you load the page. In this situation,
[success handlers](https://developers.google.com/apps-script/guides/html/communication#success_handlers) and [failure handlers](https://developers.google.com/apps-script/guides/html/communication#failure_handlers)
help control the flow of your code.

The `google.script.run` API allows 10 concurrent calls to server functions. If
you make an 11th call while 10 are still running, the server function is
delayed until one of the 10 spots is freed. In practice, you should rarely have
to think about this restriction, especially since most browsers already limit
the number of concurrent requests to the same server at a number lower than 10.
In Firefox, for example, the limit is 6. Most browsers similarly delay excess
server requests until one of the existing requests has completed.

## Parameters and return values

Call a server function with parameters from the client. Similarly, a
server function can return a value to the client as a parameter passed to a
[success handler](https://developers.google.com/apps-script/guides/html/communication#success_handlers).

Legal parameters and return values are JavaScript primitives like a `Number`,
`Boolean`, `String`, or `null`, as well as JavaScript objects and arrays that
are composed of primitives, objects and arrays. A `form` element within the page
is also legal as a parameter, but it must be the function's only parameter, and
it is not legal as a return value. Requests fail if you attempt to pass a
`Date`, `Function`, DOM element besides a `form`, or other prohibited type,
including prohibited types inside objects or arrays. Objects that create
circular references also fail, and undefined fields within arrays become
`null`.

Note that an object passed to the server becomes a copy of the original. If a
server function receives an object and changes its properties, the properties on
the client are not affected.

## Success handlers

Because `google.script.run` calls are asynchronous, client-side code continues
to the next line without waiting for a response. To specify a callback
function that runs when the server responds, use
[`withSuccessHandler(function)`](https://developers.google.com/apps-script/guides/html/reference/run#withSuccessHandler(Function)).
If the server function returns a value, the API passes that value to the
callback function as a parameter.

The following example displays a browser alert when the server responds. This
code sample requires authorization because the server-side function accesses
your Gmail account. To authorize the script, run the
`getUnreadEmails` function manually from the script editor once before you load
the page. Alternatively, when you
[deploy the web app](https://developers.google.com/apps-script/execution_web_apps#deploying) to
execute as the "user accessing the web app," you're prompted for authorization
when loading the app.

### Code.gs

```html
function doGet() {
  return HtmlService.createHtmlOutputFromFile('Index');
}

function getUnreadEmails() {
  return GmailApp.getInboxUnreadCount();
}
```

### Index.html

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <script>
      function onSuccess(numUnread) {
        var div = document.getElementById('output');
        div.innerHTML = 'You have ' + numUnread
            + ' unread messages in your Gmail inbox.';
      }

      google.script.run.withSuccessHandler(onSuccess)
          .getUnreadEmails();
    </script>
  </head>
  <body>
    <div id="output"></div>
  </body>
</html>
```

## Failure handlers

If the server fails to respond or throws an error,
[`withFailureHandler(function)`](https://developers.google.com/apps-script/guides/html/reference/run#withFailureHandler(Function))
lets you specify a failure handler to run in place of a success handler.
If an error occurs, the API passes the
[`Error`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)
object as an argument to the failure handler.

By default, if you don't specify a failure handler, failures are logged to the
JavaScript console. To override this, call `withFailureHandler(null)` or supply
a failure handler that does nothing.

The syntax for failure handlers is nearly identical to success handlers, as this
example shows.

### Code.gs

```html
function doGet() {
  return HtmlService.createHtmlOutputFromFile('Index');
}

function getUnreadEmails() {
  // 'got' instead of 'get' throws an error.
  return GmailApp.gotInboxUnreadCount();
}
```

### Index.html

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <script>
      function onFailure(error) {
        var div = document.getElementById('output');
        div.innerHTML = "ERROR: " + error.message;
      }

      google.script.run.withFailureHandler(onFailure)
          .getUnreadEmails();
    </script>
  </head>
  <body>
    <div id="output"></div>
  </body>
</html>
```

## User objects

To reuse the same success or failure handler for multiple calls to the
server, call
[`withUserObject(object)`](https://developers.google.com/apps-script/guides/html/reference/run#withUserObject(Object))
to specify an object that's passed to the handler as a second parameter.
This "user object," not to be confused with the
[`User`](https://developers.google.com/apps-script/reference/base/user) class, lets you respond to the
context in which the client contacted the server. Because user objects aren't
sent to the server, they can be most things, including functions and DOM
elements, without the restrictions on parameters and return values
for server calls. User objects can't be objects constructed with the
`new` operator.

In this example, clicking either of two buttons updates that button with a
value from the server while leaving the other button unchanged, even though they
share one success handler. Inside the `onclick` handler, the keyword `this`
refers to the `button` itself.

### Code.gs

```html
function doGet() {
  return HtmlService.createHtmlOutputFromFile('Index');
}

function getEmail() {
  return Session.getActiveUser().getEmail();
}
```

### Index.html

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <script>
      function updateButton(email, button) {
        button.value = 'Clicked by ' + email;
      }
    </script>
  </head>
  <body>
    <input type="button" value="Not Clicked"
      onclick="google.script.run
          .withSuccessHandler(updateButton)
          .withUserObject(this)
          .getEmail()" />
    <input type="button" value="Not Clicked"
      onclick="google.script.run
          .withSuccessHandler(updateButton)
          .withUserObject(this)
          .getEmail()" />
  </body>
</html>
```

## Forms

If you call a server function with a `form` element as a parameter, the form
becomes a single object with field names as keys and field values as values. The
values are all converted to strings, except for the contents of file-input
fields, which become [`Blob`](https://developers.google.com/apps-script/reference/base/blob) objects.

This example processes a form, including a file-input field, without reloading
the page; it uploads the file to Google Drive and then prints the URL for the
file in the client-side page. Inside the `onsubmit` handler, the keyword `this`
refers to the form itself. Note that upon loading all forms in the page have
the default submit action disabled by `preventFormSubmit`. This prevents the
page from redirecting to an inaccurate URL in the event of an exception.

### Code.gs

```html
function doGet() {
  return HtmlService.createHtmlOutputFromFile('Index');
}

function processForm(formObject) {
  var formBlob = formObject.myFile;
  var driveFile = DriveApp.createFile(formBlob);
  return driveFile.getUrl();
}
```

### Index.html

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <script>
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

      function handleFormSubmit(formObject) {
        google.script.run.withSuccessHandler(updateUrl).processForm(formObject);
      }
      function updateUrl(url) {
        var div = document.getElementById('output');
        div.innerHTML = '<a href="' + url + '">Got it!</a>';
      }
    </script>
  </head>
  <body>
    <form id="myForm" onsubmit="handleFormSubmit(this)">
      <input name="myFile" type="file" />
      <input type="submit" value="Submit" />
    </form>
    <div id="output"></div>
 </body>
</html>
```

## Script runners

Think of `google.script.run` as a builder for a "script runner." If you
add a success handler, failure handler, or user object to a script runner, you
aren't changing the existing runner; instead, you get back a new script runner
with new behavior.

Use any combination and any order of `withSuccessHandler`,
`withFailureHandler`, and `withUserObject`. Also call any of the
modifying functions on a script runner that already has a value set. The new
value overrides the previous value.

This example sets a common failure handler for all three server calls, but two
separate success handlers:

    var myRunner = google.script.run.withFailureHandler(onFailure);
    var myRunner1 = myRunner.withSuccessHandler(onSuccess);
    var myRunner2 = myRunner.withSuccessHandler(onDifferentSuccess);

    myRunner1.doSomething();
    myRunner1.doSomethingElse();
    myRunner2.doSomething();

## Private functions

Server functions whose names end with an underscore are considered private.
These functions cannot be called by `google.script` and their names are never
sent to the client. You can use them to hide implementation details that
need to be kept secret on the server. `google.script` also cannot see
functions within [libraries](https://developers.google.com/apps-script/guides/libraries) or functions not
declared at the top level of the script.

In this example, the function `getBankBalance` is available in the client
code; a user who inspects your source code can discover its name even if you
don't call it. However, the functions `deepSecret_` and `obj.objectMethod`
are completely invisible to
the client.

### Code.gs

```html
function doGet() {
  return HtmlService.createHtmlOutputFromFile('Index');
}

function getBankBalance() {
  var email = Session.getActiveUser().getEmail()
  return deepSecret_(email);
}

function deepSecret_(email) {
 // Do some secret calculations
 return email + ' has $1,000,000 in the bank.';
}

var obj = {
  objectMethod: function() {
    // More secret calculations
  }
};
```

### Index.html

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <script>
      function onSuccess(balance) {
        var div = document.getElementById('output');
        div.innerHTML = balance;
      }

      google.script.run.withSuccessHandler(onSuccess)
          .getBankBalance();
    </script>
  </head>
  <body>
    <div id="output">No result yet...</div>
  </body>
</html>
```

## Resize dialogs in Google Workspace applications

[Custom dialog boxes](https://developers.google.com/apps-script/guides/dialogs) in Google Docs,
Google Sheets, or Forms can be resized by calling the
[`google.script.host`](https://developers.google.com/apps-script/guides/html/reference/host) methods
[`setWidth(width)`](https://developers.google.com/apps-script/guides/html/reference/host#setWidth(int)) or
[`setHeight(height)`](https://developers.google.com/apps-script/guides/html/reference/host#setHeight(int)) in
client-side code. (To set the initial size of a dialog, use the `HtmlOutput`
methods
[`setWidth(width)`](https://developers.google.com/apps-script/reference/html/html-output#setWidth(Integer))
and
[`setHeight(height)`](https://developers.google.com/apps-script/reference/html/html-output#setHeight(Integer)).)
Note that dialogs don't re-center in the parent window when resized, and it is
not possible to resize [sidebars](https://developers.google.com/apps-script/guides/dialogs#custom_sidebars).

## Close dialogs and sidebars in Google Workspace

If you use the HTML service to display a [dialog or
sidebar](https://developers.google.com/apps-script/guides/dialogs) in Google Docs, Sheets,
or Forms, you cannot close the interface by calling
`window.close`. Instead, you must call
[`google.script.host.close`](https://developers.google.com/apps-script/guides/html/reference/host#close()).
For an example, see the section on [serving HTML as a Google Workspace
user
interface](https://developers.google.com/apps-script/guides/html#serve_html_as_a_google_docs_sheets_or_forms_user_interface).

## Move browser focus in Google Workspace

To switch focus in the user's browser from a dialog or sidebar back to the
Google Docs, Sheets, or Forms editor, call the
method
[`google.script.host.editor.focus`](https://developers.google.com/apps-script/guides/html/reference/host#editor.focus()).
This method is particularly useful in combination with the [Document
service](https://developers.google.com/apps-script/reference/document) methods [`Document.setCursor(position)`](https://developers.google.com/apps-script/reference/document/document#setCursor(Position))
and
[`Document.setSelection(range)`](https://developers.google.com/apps-script/reference/document/document#setSelection(Range)).

# HTML Service: Templated HTML

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
`<?= ... ?>` tag (a [print scriptlet](https://developers.google.com/apps-script/guides/html/templates#print_scriptlets)) appear in
italics. This code runs on the server before the page is served
to the user. Because scriptlet code executes before the page is served, it
can only run once per page. Unlike client-side JavaScript or
Apps Script functions that you call through
[`google.script.run`](https://developers.google.com/apps-script/guides/html/communication), scriptlets can't
execute again after the page loads.

### Code.gs

    function doGet() {
      return HtmlService
          .createTemplateFromFile('Index')
          .evaluate();
    }

### Index.html

    <!DOCTYPE html>
    <html>
      <head>
        <base target="_top">
      </head>
      <body>
        Hello, World! The time is <?= new Date() ?>.
      </body>
    </html>

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

### Code.gs

    function doGet() {
      return HtmlService
          .createTemplateFromFile('Index')
          .evaluate();
    }

### Index.html

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

### Print scriptlets

Printing scriptlets, which use the syntax `<?= ... ?>`, output the results of
their code into the page using contextual escaping.

Contextual escaping means that Apps Script keeps track of the
output's context on the page --- inside an HTML attribute, inside a client-side
`script` tag, or anywhere else --- and automatically adds escape characters [to
protect against cross-site scripting (XSS)
attacks](https://developers.google.com/closure/templates/docs/security).

In this example, the first printing scriptlet outputs a string directly; it is
followed by a standard scriptlet that sets up an array and a loop, followed by
another printing scriptlet to output the contents of the array.

### Code.gs

    function doGet() {
      return HtmlService
          .createTemplateFromFile('Index')
          .evaluate();
    }

### Index.html

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

### Code.gs

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

### Index.html

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

### Call Apps Script APIs directly

You can also use Apps Script code directly in scriptlets. This
example accomplishes the same result as the previous example by loading the
data in the template itself rather than through a separate function.

### Code.gs

    function doGet() {
      return HtmlService
          .createTemplateFromFile('Index')
          .evaluate();
    }

### Index.html

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

### Push variables to templates

Lastly, you can push variables into a template by assigning them as properties
of the [`HtmlTemplate`](https://developers.google.com/apps-script/reference/html/html-template) object. Once
again, this example accomplishes the same result as the previous examples.

### Code.gs

    function doGet() {
      var t = HtmlService.createTemplateFromFile('Index');
      t.data = SpreadsheetApp
          .openById('1234567890abcdefghijklmnopqrstuvwxyz')
          .getActiveSheet()
          .getDataRange()
          .getValues();
      return t.evaluate();
    }

### Index.html

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

### Code.gs

    function myFunction() {
      Logger.log(HtmlService
          .createTemplateFromFile('Index')
          .getCode());
    }

### Index.html

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

### LOG (EVALUATED)

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

# HTML Service: Restrictions

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
- `allow-top-navigation-by-user-activation` - This attribute is only set for [stand-alone script projects](https://developers.google.com/apps-script/guides/standalone).

The `allow-top-navigation` keyword, which allows the content to navigate its
top-level browsing context, is restricted and not set as an attribute in the
sandbox. If you need to redirect your script, add a link or a button for the
user to take action on instead.

### Set the link target attribute

In the `IFRAME` mode you need to set the link target attribute to either
`_top` or `_blank`:

### Code.js

    function doGet() {
      var template = HtmlService.createTemplateFromFile('top');
      return template.evaluate().setSandboxMode(HtmlService.SandboxMode.IFRAME);
    }

### top.html

    <!DOCTYPE html>
    <html>
     <body>
       <div>
         <a href="http://google.com" target="_top">Click Me!</a>
       </div>
     </body>
    </html>

You can also override this attribute using the `<base>` tag within the head
section of the enclosing web page:

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

### HTTPS required for active content

["Active"
content](https://developer.mozilla.org/en-US/docs/Security/MixedContent#Mixed_active_content)
like scripts, external stylesheets, and XmlHttpRequests must be loaded over
HTTPS, not HTTP.

# Migrate to IFRAME Sandbox Mode

Google Apps Script uses a [security sandbox](https://developers.google.com/apps-script/guides/html/restrictions)
to provide protective isolation for Google Workspace applications in
certain situations. All sandbox modes are now sunset except for `IFRAME`. Apps
using older sandbox modes now use the newer `IFRAME` mode automatically.

Apps that previously used these older modes with the HTML Service may need to
make changes for `IFRAME` mode, to address the following differences:

- You now must override the link's `target` attribute using `target="_top"` or `target="_blank"`
- HTML files served by the HTML Service must include \<!DOCTYPE html\>, \<html\>, and \<body\> tags
- The `gapi` loader library (`api.js`) doesn't load automatically in `IFRAME` mode
- [Picker](https://developers.google.com/apps-script/guides/dialogs#file-open_dialogs) users need to call `setOrigin` because content is served from a new domain
- Some older browsers, including IE9, are not supported
- Imported resources must now use HTTPS
- Form submission are no longer prevented by default

These differences are detailed in the following sections.

## Set the link target attribute

In the `IFRAME` mode you need to set the link target attribute to either `_top`
or `_blank`:

### Code.js

    function doGet() {
      var template = HtmlService.createTemplateFromFile('top');
      return template.evaluate();
    }

### top.html

    <!DOCTYPE html>
    <html>
     <body>
       <div>
         <a href="http://google.com" target="_top">Click Me!</a>
       </div>
     </body>
    </html>

You can also override this attribute using the \<base\> tag within the head
section of the enclosing web page:

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

## Top-level HTML tags

Under `NATIVE` (and `EMULATED`) sandbox mode, certain HTML tags would be
automatically added to an Apps Script .html file, but this does
not happen when using `IFRAME` mode.

To make sure your project pages are served correctly using `IFRAME`, wrap your
page content in the following top-level tags:

    <!DOCTYPE html>
    <html>
      <body>
        <!-- Add your HTML content here -->
      </body>
    </html>

## The gapi loader library must be explicitly loaded

Scripts that relied on automatic loading of the `gapi` loader library (`api.js`)
must be changed to load this library explicitly, as in the following example:

    <script src="https://apis.google.com/js/api.js?onload=onApiLoad">
    </script>

## Google Picker API change

When using the [Google Picker API](https://developers.google.com/apps-script/guides/dialogs#file-open_dialogs),
you must now call `setOrigin` when constructing the PickerBuilder and pass in
the origin `google.script.host.origin`, as shown in the following example:

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

A complete example can be found on the HtmlService guide
[Client-to-Server Communication](https://developers.google.com/apps-script/guides/html/communication#forms).

# Web Apps

Publish the script as a web app if you build a user interface for it. For
example, a script that lets users schedule appointments with members of a
support team is best presented as a web app so that users access it directly
from their browsers.

Both [standalone scripts](https://developers.google.com/apps-script/guides/standalone) and [scripts bound to
Google Workspace applications](https://developers.google.com/apps-script/guides/bound) can be turned into
web apps, so long as they meet the following requirements.

## Requirements for web apps

A script can be published as a web app if it meets these requirements:

- It contains a `doGet` or `doPost` function.
- The function returns an [HTML service](https://developers.google.com/apps-script/guides/html) [`HtmlOutput`](https://developers.google.com/apps-script/reference/html/html-output) object or a [Content service](https://developers.google.com/apps-script/guides/content) [`TextOutput`](https://developers.google.com/apps-script/reference/content/text-output) object.

## Request parameters

When a user visits an app or a program sends the app an HTTP `GET` request,
Google Apps Script runs the function `doGet`. When a program sends the app
an HTTP `POST` request, Apps Script runs `doPost` instead. In
both cases, the `e` argument represents an event parameter that can contain
information about any request parameters. The structure of the event object is
shown in the following table:

| Fields ||
|---|---|
| `e.queryString` | The value of the query string portion of the URL, or `null` if no query string is specified ``` name=alice&n=1&n=2 ``` |
| `e.parameter` | An object of key/value pairs that correspond to the request parameters. Only the first value is returned for parameters that have multiple values. ``` {"name": "alice", "n": "1"} ``` |
| `e.parameters` | An object similar to `e.parameter`, but with an array of values for each key ``` {"name": ["alice"], "n": ["1", "2"]} ``` |
| `e.pathInfo` | The URL path after `/exec` or `/dev`. For example, if the URL path ends in `/exec/hello`, the path info is `hello`. |
| `e.contextPath` | Not used, always the empty string. |
| `e.contentLength` | The length of the request body for POST requests, or `-1` for GET requests ``` 332 ``` |
| `e.postData.length` | The same as `e.contentLength` ``` 332 ``` |
| `e.postData.type` | The MIME type of the POST body ``` text/csv ``` |
| `e.postData.contents` | The content text of the POST body ``` Alice,21 ``` |
| `e.postData.name` | Always the value "postData" ``` postData ``` |

Pass parameters such as `username` and `age` to a URL like the following:

    https://script.google.com/.../exec?username=jsmith&age=21

Display the parameters like so:

    function doGet(e) {
      var params = JSON.stringify(e);
      return ContentService.createTextOutput(params).setMimeType(ContentService.MimeType.JSON);
    }

In the preceding example, `doGet` returns the following output:

    {
      "queryString": "username=jsmith&age=21",
      "parameter": {
        "username": "jsmith",
        "age": "21"
      },
      "contextPath": "",
      "parameters": {
        "username": [
          "jsmith"
        ],
        "age": [
          "21"
        ]
      },
      "contentLength": -1
    }

The following parameter names are reserved by the system and shouldn't
be used in URL parameters or POST bodies:

- `c`
- `sid`

Using these parameters can result in an HTTP 405 response with the error message
"Sorry, the file you have requested does not exist." If possible, update your
script to use different parameter names.

## Deploy a script as a web app

To deploy a script as a web app, follow these steps:

1. At the top right of the script project, click **Deploy** \> **New deployment**.
2. Next to "Select type," click Enable deployment types \> **Web app**.
3. Enter the information about your web app in the fields under "Deployment configuration."
4. Click **Deploy**.

Share the web app URL with those you would like to use your app, provided you
have granted them access.

Web apps deployed in one domain cease to function if their ownership
changes to a
[shared drive](https://developers.google.com/apps-script/guides/collaborating#collaborating_with_shared_drives)
or account in a different domain. This can be corrected by having the
new owner or collaborator redeploy the web app in the new domain. Alternatively,
if the web app is moved back to its original domain the web app starts
functioning again for that domain without redeploying.

## Test a web app deployment

To test your script as a web app, follow the steps below:

1. At the top right of the script project, click **Deploy \> Test
   deployments**.
2. Next to "Select type," click Enable deployment types **\> Web app**.
3. Under the web app URL, click **Copy**.
4. Paste the URL in your browser and test your web app.

   This URL ends in `/dev` and can only be accessed by users who have edit access
   to the script. This instance of the app always runs the most recently saved
   code and is only intended for testing during development.

To test [granular OAuth](https://developers.google.com/apps-script/concepts/scopes#handle-granular) feature on the
web app, make sure that your project doesn't already have some authorizations.
To invalidate any existing authorizations use
[ScriptApp.invalidateAuth](https://developers.google.com/apps-script/reference/script/script-app#invalidateauth).
For any web apps that are already deployed and running
[under the identity of the active user](https://developers.google.com/apps-script/guides/web#permissions), modify the `executeAs`
JSON field in the [manifest](https://developers.google.com/apps-script/concepts/manifests#editing_a_manifest)
to `USER_DEPLOYING`.

When deploying web apps to run as the developer, exercise great care when
handling OAuth tokens obtained through
[ScriptApp.getOAuthToken](https://developers.google.com/apps-script/reference/script/script-app#getoauthtoken).
These tokens can grant other applications access to your data --- never
transmit them to the client.

## Permissions

The permissions for a web app differ depending how you choose to execute
the app:

- **Execute the app as me**---In this case, the script always executes as you, the owner of the script, no matter who accesses the web app.
- **Execute the app as user accessing the web app**---In this case, the script runs under the identity of the active user using the web app. This permission approach causes the web app to show the email of the script owner when the user authorizes access.

To prevent abuse, Apps Script imposes limits on the rate at which
new users can authorize a web app that executes as the user. These limits
depend, among other factors, on whether the publishing account is part of a
[Google Workspace](https://gsuite.google.com/) domain.

Collaborate on web apps using
[shared drive](https://developers.google.com/apps-script/guides/collaborating#collaborating_with_shared_drives).
When a web app in a shared drive is deployed, choosing to "execute as you"
causes the web app to execute under the authority of the user that deployed it
(since there is no script owner).

## Embed your web app in Google Sites {:#embed-web-app}

Embedded web apps are still subject to access permissions to prevent malicious
use. If your embedded web app doesn't seem to be working, check to see if the
permissions set by the web app owner and the domain administrator allow its use.

In order to embed a web app in Sites, it must first be
[deployed](https://developers.google.com/apps-script/guides/web#deploying_a_script_as_a_web_app). You also need the **Deployed URL**
from the **Deploy** dialog.

To embed a web app into a [Sites](https://sites.google.com/new)
page, follow these steps:

1. Open the Sites page where you'd like to add the web app.
2. Select **Insert \> Embed URL**.
3. Paste in the web app URL and then click **ADD**.

The web app appears in a frame in the page's preview. When you publish the page,
your site viewers may need to authorize the web app before it executes
normally. Unauthorized web apps present authorization prompts to the user.

## Web Apps and Browser History

To simulate a multi-page application, or one with a dynamic UI controlled using
URL parameters, define a state object to represent the app's UI or page, and
push the state into the browser history as the user navigates your app. Listen
to history events so that your web app displays the correct UI when the user
navigates back and forth with the browser buttons. By querying the URL
parameters at load time, have your app dynamically build its UI based on those
parameters, allowing the user to start the app in a particular state.

Apps Script provides two asynchronous client-side JavaScript APIs
to assist with creating web apps that are linked to the browser history:

- [`google.script.history`](https://developers.google.com/apps-script/guides/html/reference/history)
  provides methods to allow dynamic response to browser history changes. This
  includes: pushing states (simple Objects you define) onto the browser
  history, replacing the top state in the history stack, and setting a listener
  callback function to respond to history changes.

- [`google.script.url`](https://developers.google.com/apps-script/guides/html/reference/url) provides
  the means to retrieve the current page's URL parameters and URL fragment, if
  they are present.

These history APIs are only available to web apps. They are not supported for
sidebars, dialogs or add-ons. This functionality is also not
recommended for use in [web apps embedded in a Sites](https://developers.google.com/apps-script/guides/web#embedding_your_web_app_in_google_sites).

# HTML Service: Best Practices

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

### Code.gs

```html
function doGet(request) {
  return HtmlService.createTemplateFromFile('Page')
      .evaluate();
}

function include(filename) {
  return HtmlService.createHtmlOutputFromFile(filename)
      .getContent();
}
```

### Page.html

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

### Stylesheet.html

```html
<style>
p {
  color: green;
}
</style>
```

### JavaScript.html

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

No --- load in templates

```html
<p>List of things:</p>
<? var things = getLotsOfThings(); ?>
<ul>
  <? for (var i = 0; i < things.length; i++) { ?>
    <li><?= things[i] ?></li>
  <? } ?>
</ul>
```

Yes --- load asynchronously

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
> Mixed Content: The page at 'https://...' was loaded over HTTPS, but
> requested an insecure script 'http://...'. This request has been blocked;
> the content must be served over HTTPS.

Most popular libraries support both HTTP and HTTPS, so switching is usually
just a matter of inserting an addition 's' into the URL.

## Use the HTML5 document type declaration

If your page is served using the newer `IFRAME`
[sandbox mode](https://developers.google.com/apps-script/guides/html/restrictions#sandbox_mode), make sure
to include the following snippet of code at the top of your HTML file.

    <!DOCTYPE html>

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

