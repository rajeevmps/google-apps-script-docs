# Custom Functions in Google Sheets

## Page Summary

- Google Sheets allows creating custom functions using Google Apps Script in JavaScript to extend built-in functionalities.
- To create a custom function, write JavaScript code in the script editor accessed through the Extensions menu in Google Sheets.
- Custom functions can take arguments, return values, and work with various data types supported by JavaScript.
- Custom functions can be shared by copying the script to other spreadsheets or publishing them as add-ons.
- Optimizing custom functions by processing ranges as arrays can significantly improve performance for large datasets.

Google Sheets offers hundreds of
[built-in functions](https://support.google.com/drive/topic/1361471) like
[`AVERAGE`](https://support.google.com/drive/answer/3093615),
[`SUM`](https://support.google.com/drive/answer/3093669), and
[`VLOOKUP`](https://support.google.com/drive/answer/3093318). When these aren't
enough for your needs, you can use Apps Script to write custom
functions then use them in Sheets just like a built-in function.

For examples of custom functions, see the following tutorials:

- [Calculate sale price of discounted items (quickstart)](https://developers.google.com/apps-script/quickstart/custom-functions)
- [Calculate a tiered pricing discount](https://developers.google.com/apps-script/samples/custom-functions/tier-pricing)
- [Calculate driving distance & convert meters to miles](https://developers.google.com/apps-script/samples/custom-functions/calculate-driving-distance)
- [Summarize data from multiple sheets](https://developers.google.com/apps-script/samples/custom-functions/summarize-sheets-data)
- [Fact-check statements with an ADK AI agent and Gemini model](https://developers.google.com/apps-script/samples/custom-functions/fact-check)

## Getting started

Custom functions are created using standard JavaScript. If you're new to
JavaScript, Codecademy offers a
[course for beginners](https://www.codecademy.com/learn/introduction-to-javascript).
This course wasn't developed by and isn't associated with Google.

Here's a custom function, named `DOUBLE`, which multiplies an
input value by 2:

```javascript
/**
 * Multiplies an input value by 2.
 * @param {number} input The number to double.
 * @return The input multiplied by 2.
 * @customfunction
*/
function DOUBLE(input) {
  return input * 2;
}
```

If you don't know how to write JavaScript and don't have time to learn,
check the Google Workspace add-on store to
see whether someone else has already built the custom function you need.

### Create a custom function

To write a custom function:

1. [Create](https://docs.google.com/spreadsheets/create)
or open a spreadsheet in Sheets.
2. Select the menu item **Extensions** >
**Apps Script**.
3. Delete any code in the script editor. For the `DOUBLE` function shown
earlier, copy and paste the code into the script editor.
4. At the top, click Save save.

Now you can use the custom function.

### Get a custom function from the Google Workspace Marketplace

The Google Workspace Marketplace offers several custom functions as
[Google Workspace add-ons for
Sheets](https://support.google.com/drive/answer/3641454).
To use or explore these add-ons:

1. [Create](https://docs.google.com/spreadsheets/create)
or open a spreadsheet in Sheets.
2. At the top, click **Add-ons > Get add-ons**.
3. Once the [Google Workspace Marketplace](https://workspace.google.com/marketplace)
opens, click the search box in the top right corner.
4. Type "custom function" and press Enter.
5. If you find a custom function add-on you're interested in, click **Install**
to install it.
6. A dialog might tell you that the add-on requires authorization. If so,
read the notice carefully, then click **Allow**.
7. The add-on becomes available in the spreadsheet. To use the add-on in a
different spreadsheet, open the other spreadsheet and at the top, click
**Add-ons > Manage add-ons**. Find the add-on you want to use and click
Options more_vert > **Use in this
document**.

### Use a custom function

Once you've written a custom function or installed one from the
Google Workspace Marketplace, it's used just like a built-in function:

1. Click the cell where you want to use the function.
2. Type an equals sign (`=`) followed by the function name and any input value —
for example, `=DOUBLE(A1)` — and press Enter.
3. The cell momentarily displays `Loading...`, then returns the result.

## Guidelines for custom functions

Before writing your own custom function, there are a few guidelines to know.

### Function naming

In addition to the standard conventions for naming JavaScript functions, be
aware of the following:

- The name of a custom function must be distinct from the names of
[built-in functions](https://support.google.com/docs/table/25273) like
`SUM()`.
- The name of a custom function can't end with an underscore (`_`), which
denotes a private function in Apps Script.
- The name of a custom function must be declared with the syntax
`function myFunction()`, not `var myFunction = new Function()`.
- Capitalization doesn't matter, although the names of spreadsheet functions
are traditionally uppercase.

### Arguments

Like a built-in function, a custom function can take arguments as input values:

- If you call your function with a reference to a single cell as an argument
(like `=DOUBLE(A1)`), the argument is the value of the cell.
- If you call your function with a reference to a range of cells as an
argument (like `=DOUBLE(A1:B10)`), the argument is a two-dimensional
array of the cells' values. For example, in the following screenshot, the
arguments in `=DOUBLE(A1:B2)` are interpreted by Apps Script as
`double([[1,3],[2,4]])`. Note that the sample code for `DOUBLE`
described earlier would need to be
modified to accept an array as input.
- Custom function arguments must be
[deterministic](http://en.wikipedia.org/wiki/Deterministic_algorithm). That
is, built-in spreadsheet functions that return a different result each time
they calculate — such as `NOW()` or `RAND()` — are not allowed as arguments
to a custom function. If a custom function tries to return a value based on
one of these volatile built-in functions, it displays `Loading...`
indefinitely.
- To trigger recalculation, you must pass a referenced cell or cell range
directly as an argument to the custom function. Otherwise, the custom
function doesn't recalculate until you edit the function, or you change
the value of a referenced cell. If you use the `getValue` method in custom
functions, be aware that the referenced range isn't directly passed as an
argument to the custom function.

### Return values

Every custom function must return a value to display, such that:

- If a custom function returns a value, the value displays in the cell
the function was called from.
- If a custom function returns a two-dimensional array of values, the values
overflow into adjacent cells as long as those cells are empty. If this would
cause the array to overwrite existing cell contents, the custom function
throws an error instead. For an example, see the section on
optimizing custom functions.
- A custom function can't affect cells other than those it returns a value to.
In other words, a custom function can't edit arbitrary cells, only the
cells it is called from and their adjacent cells. To edit arbitrary cells,
use a [custom menu](https://developers.google.com/apps-script/guides/menus) to run a function instead.
- A custom function call must return within 30 seconds. If it doesn't, the
cell displays `#ERROR!` and the cell note is `Exceeded maximum execution time
(line 0).`

### Data types

Sheets stores data in
[different formats](https://support.google.com/docs/answer/56470) depending on
the nature of the data. When these values are used in custom functions,
Apps Script treats them as the
[appropriate data type in JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures).
These are the most common areas of confusion:

- Times and dates in Sheets become
[Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) objects in Apps Script. If the
spreadsheet and the
script use different time zones (a rare problem), the custom function needs to
compensate.
- Duration values in Sheets also become `Date` objects, but
[working with them can be complicated](http://stackoverflow.com/questions/17715841/gas-how-to-read-the-correct-time-values-form-google-spreadsheet).
- Percentage values in Sheets become decimal numbers in Apps Script. For
example, a cell with a value of `10%` becomes `0.1` in
Apps Script.

### Autocomplete

Sheets supports autocomplete for custom functions much like for
[built-in functions](https://support.google.com/docs/answer/91932). As you
type a function name in a cell, you see a list of built-in and custom
functions that matches what you enter.

Custom functions appear in this list if their script includes a
[JSDoc](https://developers.google.com/apps-script/concepts/jsdoc) `@customfunction` tag, as in the `DOUBLE()`
example.

```javascript
/**
 * Multiplies the input value by 2.
 *
 * @param {number} input The value to multiply.
 * @return {number} The input multiplied by 2.
 * @customfunction
 */
function DOUBLE(input) {
  return input * 2;
}
```

## Advanced

This section covers advanced custom function topics.

### Use Google Apps Script services

Custom functions can call certain
[Apps Script services](https://developers.google.com/apps-script/guides/services) to perform
more complex tasks. For example, a custom function can call the
[Language](https://developers.google.com/apps-script/reference/language) service to translate an English
phrase into Spanish.

Unlike most other types of Apps Scripts, custom functions never ask users to
authorize access to personal data. Consequently, they can only call services
that don't have access to personal data, specifically the following:

| [Cache](https://developers.google.com/apps-script/reference/cache) | Works, but not particularly useful in custom functions |
|---|---|
| [HTML](https://developers.google.com/apps-script/reference/html) | Can generate HTML, but can't display it (rarely useful) |
| [JDBC](https://developers.google.com/apps-script/reference/jdbc) |  |
| [Language](https://developers.google.com/apps-script/reference/language) |  |
| [Lock](https://developers.google.com/apps-script/reference/lock) | Works, but not particularly useful in custom functions |
| [Maps](https://developers.google.com/apps-script/reference/maps) | Can calculate directions, but not display maps |
| [Properties](https://developers.google.com/apps-script/reference/properties) | `getUserProperties()` only gets the properties of the spreadsheet owner. Spreadsheet editors can't set user properties in a custom function. |
| [Spreadsheet](https://developers.google.com/apps-script/reference/spreadsheet) | Read-only (can use most `get*()` methods, but not `set*()` ). Cannot open other spreadsheets ( `SpreadsheetApp.openById()` or `SpreadsheetApp.openByUrl()` ). |
| [URL Fetch](https://developers.google.com/apps-script/reference/url-fetch) | Access resources on the web by fetching URLs. |
| [Utilities](https://developers.google.com/apps-script/reference/utilities) |  |
| [XML](https://developers.google.com/apps-script/reference/xml-service) |  |

If your custom function throws the error message `You do not have permission to
call X service.`, the service requires user authorization and thus can't be
used in a custom function.

To use a service other than those in the preceding list, create a
[custom menu](https://developers.google.com/apps-script/guides/menus) that runs an
Apps Script function
instead of writing a custom function. A function that is triggered from a menu
asks the user for authorization if necessary and can consequently use all
Apps Script services.

### Share custom functions

Custom functions start out [bound](https://developers.google.com/apps-script/guides/bound) to the
spreadsheet they were created in. This means that a custom function written in
one spreadsheet can't be used in other spreadsheets unless you use one of the
following methods:

- Click **Extensions** > **Apps Script** to
open the script editor, then copy the
script text from the original spreadsheet and paste it into the script editor
of another spreadsheet.
- Make a copy of the spreadsheet that contains the custom function by clicking
**File > Make a copy**. When a spreadsheet is copied, any scripts attached to
it are copied as well. Anyone who has access to the spreadsheet can copy the
script. (Collaborators who have only view access can't open the script editor
in the original spreadsheet. However, when they make a copy, they become the
owner of the copy and can see the script.)
- Publish the script as a Sheets [Editor add-on](https://developers.google.com/apps-script/add-ons/how-tos/building-editor-addons).

All container-bound scripts share the same access lists as their containers.
This means that anyone with permission to edit the spreadsheet can also edit
any Apps Script code attached to it. For more information, see
[access to bound scripts](https://developers.google.com/apps-script/guides/bound#access_to_bound_scripts).

### Optimization

Each time a custom function is used in a spreadsheet, Sheets
makes a separate call to the Apps Script server. If your
spreadsheet contains dozens (or hundreds, or thousands!) of custom function
calls, this process can be slow. Some projects with many or complex custom
functions might experience a temporary delay in executions.

Consequently, if you plan to use a custom function multiple times on a large
range of data, consider modifying the function so that it accepts a range as
input in the form of a two-dimensional array, then returns a two-dimensional
array that can overflow into the appropriate cells.

For example, the `DOUBLE()` function shown earlier can be rewritten to accept a
single cell or range of cells as follows:

```javascript
/**
 * Multiplies the input value by 2.
 *
 * @param {number|Array<Array<number>>} input The value or range of cells
 *     to multiply.
 * @return The input multiplied by 2.
 * @customfunction
 */
function DOUBLE(input) {
  return Array.isArray(input) ?
      input.map(row => row.map(cell => cell * 2)) :
      input * 2;
}
```

This approach uses the
[map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
method of JavaScript's `Array` object on the two-dimensional array of
cells to get each row, then for each row, it uses `map` again to return double
each cell's value. It returns a two-dimensional array that contains the results.
This way, you can call `DOUBLE` just once but have it calculate for a large
number of cells at once, as shown in the following screenshot. You could
accomplish the same thing with nested `if` statements instead of the `map`
call.

![](https://developers.google.com/static/apps-script/images/custom-functions-example.png)

Similarly, the following custom function efficiently fetches live content from
the Internet and uses a two-dimensional array to display two columns of results
with just a single function call. If each cell required its own function call,
the operation would take considerably more time, since the
Apps Script server would have to download and parse the XML feed
each time.

```javascript
/**
 * Show the title and date for the first page of posts on the
 * Developer blog.
 *
 * @return Two columns of data representing posts on the
 *     Developer blog.
 * @customfunction
 */
function getBlogPosts() {
  var array = [];
  var url = 'https://gsuite-developers.googleblog.com/atom.xml';
  var xml = UrlFetchApp.fetch(url).getContentText();
  var document = XmlService.parse(xml);
  var root = document.getRootElement();
  var atom = XmlService.getNamespace('http://www.w3.org/2005/Atom');
  var entries = document.getRootElement().getChildren('entry', atom);
  for (var i = 0; i < entries.length; i++) {
    var title = entries[i].getChild('title', atom).getText();
    var date = entries[i].getChild('published', atom).getValue();
    array.push([title, date]);
  }
  return array;
}
```

These techniques can be applied to nearly any custom function that is used
repeatedly throughout a spreadsheet, although the implementation details vary
depending on the function's behavior.
