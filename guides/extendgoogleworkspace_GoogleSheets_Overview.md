# Extend Google Sheets

Use Google Apps Script to extend Sheets. Add [custom
menus](https://developers.google.com/apps-script/guides/menus), [dialogs, and
sidebars](https://developers.google.com/apps-script/guides/dialogs) to Sheets. Write [custom
functions](https://developers.google.com/apps-script/guides/sheets/functions) for Sheets, and
integrate it with other [Google services](https://developers.google.com/apps-script/guides/services) like
Google Calendar, Google Drive, and Gmail.

Most scripts designed for Sheets manipulate arrays to interact
with the cells, rows, and columns in a spreadsheet. If you're not familiar with
arrays in JavaScript, Codecademy offers a
[great training module for arrays](https://www.codecademy.com/learn/introduction-to-javascript/modules/learn-javascript-arrays).
This course wasn't developed by and isn't associated with Google.

For a quick introduction to using Apps Script with
Sheets, see the 5-minute quickstart guide for
[Macros, Menus, and Custom Functions](https://developers.google.com/apps-script/quickstart/macros).

## Get started

Apps Script includes special APIs to programmatically create,
read, and edit Sheets. Apps Script interacts with
Sheets in two ways: any script can create or modify a spreadsheet
if the script's user has appropriate permissions for it, and a script can also
be [bound](https://developers.google.com/apps-script/guides/bound) to a spreadsheet. Bound scripts have
special abilities to alter the user interface or respond when the spreadsheet
is opened. To create a bound script, select **Extensions**
\> **Apps Script**
from within Sheets.

The [Spreadsheet service](https://developers.google.com/apps-script/reference/spreadsheet) treats Sheets
as a grid, operating with two-dimensional arrays. To retrieve data from the
spreadsheet, get access to the spreadsheet where the data is stored, get the
range that holds the data, and then get the values of the cells.
Apps Script facilitates data access by reading structured data in
the spreadsheet and creating JavaScript objects for them.

### Read data

Suppose you have a list of product names and product numbers that you store in
a spreadsheet, as shown in the following image.

![](https://developers.google.com/static/apps-script/images/spreadsheet_basics1.png)

The following example shows how to retrieve and log the product names and product
numbers.

    function logProductInfo() {
      const sheet = SpreadsheetApp.getActiveSheet();
      const data = sheet.getDataRange().getValues();
      for (let i = 0; i < data.length; i++) {
        Logger.log('Product name: ' + data[i][0]);
        Logger.log('Product number: ' + data[i][1]);
      }
    }

#### View logs

To view the data that has been logged, at the top of the script editor, click
**Execution log**.

### Write data

To store data, such as a new product name and number to the spreadsheet, add the
following code to the end of the script.

    function addProduct() {
      const sheet = SpreadsheetApp.getActiveSheet();
      sheet.appendRow(['Cotton Sweatshirt XL', 'css004']);
    }

The preceding code appends a new row at the bottom of the spreadsheet, with the
values specified. If you run this function, a new row is added to the
spreadsheet.

## Custom menus and user interfaces

Customize Sheets by adding custom menus, dialogs, and
sidebars. To learn the basics of creating menus, see the
[guide to menus](https://developers.google.com/apps-script/guides/menus). To learn about customizing the content of a dialog,
see the [guide to HTML service](https://developers.google.com/apps-script/guides/html#serve_html_as_a_google_docs_sheets_or_forms_user_interface).

Attach a script function to an image or drawing within a spreadsheet; the
function executes when a user clicks on the image or drawing. To learn more, see
[Images and Drawings in Sheets](https://developers.google.com/apps-script/guides/menus#clickable_images_and_drawings_in_google_sheets).

If you're planning to publish your custom interface as part of an
[add-on](https://developers.google.com/apps-script/guides/sheets#add-ons), follow the
[style guide](https://developers.google.com/workspace/add-ons/guides/editor-style) for consistency with the
style and layout of the Sheets editor.

## Connect to Google Forms

Connect Google Forms with Sheets through the
[Forms](https://developers.google.com/apps-script/reference/forms) and
[Spreadsheet](https://developers.google.com/apps-script/reference/spreadsheet) services. This feature automatically
creates a Google Form based on data in a spreadsheet.
Apps Script also lets you use [triggers](https://developers.google.com/apps-script/guides/sheets#triggers), such
as `onFormSubmit` to perform a specific action after a user responds to the
form. To learn more about connecting Sheets to Forms, try the
[Managing Responses for Forms](https://developers.google.com/apps-script/quickstart/forms) 5-minute
quickstart.

## Format data

The [`Range`](https://developers.google.com/apps-script/reference/spreadsheet/range) class has methods like
[`setBackground`](https://developers.google.com/apps-script/reference/spreadsheet/range#setBackground(String))
to access and modify the format of a cell or range of cells. The following
example sets the font style of a range:

    function formatMySpreadsheet() {
      // Set the font style of the cells in the range of B2:C2 to be italic.
      const ss = SpreadsheetApp.getActiveSpreadsheet();
      const sheet = ss.getSheets()[0];
      const cell = sheet.getRange('B2:C2');
      cell.setFontStyle('italic');
    }

## Data validation

Access existing data-validation rules in Sheets or create new
rules. For example, the following sample shows how to set a data-validation
rule that allows only numbers between 1 and 100 on a cell.

    function validateMySpreadsheet() {
      // Set a rule for the cell B4 to be a number between 1 and 100.
      const cell = SpreadsheetApp.getActive().getRange('B4');
      const rule = SpreadsheetApp.newDataValidation()
         .requireNumberBetween(1, 100)
         .setAllowInvalid(false)
         .setHelpText('Number must be between 1 and 100.')
         .build();
      cell.setDataValidation(rule);
    }

For more details on working with data-validation rules, see
[`SpreadsheetApp.newDataValidation`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#newDataValidation()),
[`DataValidationBuilder`](https://developers.google.com/apps-script/reference/spreadsheet/data-validation-builder),
and [`Range.setDataValidation`](https://developers.google.com/apps-script/reference/spreadsheet/range#setDataValidation(DataValidation))

## Charts

Embed charts in a spreadsheet that represent the data in a specific range. The
following example generates an embedded bar chart, assuming you have chartable
data in cells `A1:B15`:

    function newChart() {
      // Generate a chart representing the data in the range of A1:B15.
      const ss = SpreadsheetApp.getActiveSpreadsheet();
      const sheet = ss.getSheets()[0];

      const chart = sheet.newChart()
         .setChartType(Charts.ChartType.BAR)
         .addRange(sheet.getRange('A1:B15'))
         .setPosition(5, 5, 0, 0)
         .build();

      sheet.insertChart(chart);
    }

To learn more about embedding a chart into your spreadsheet, see
[`EmbeddedChart`](https://developers.google.com/apps-script/reference/spreadsheet/embedded-chart) and specific chart
builders, such as
[`EmbeddedPieChartBuilder`](https://developers.google.com/apps-script/reference/spreadsheet/embedded-pie-chart-builder).

## Custom functions in Google Sheets

A [custom function](https://developers.google.com/apps-script/guides/sheets/functions) is similar to a built-in spreadsheet
function like `=SUM(A1:A5)` except that you define the function's behavior with
Apps Script. For example, you could create a custom function,
`in2mm()`, that converts a value from inches to millimeters, then use the
formula in your spreadsheet by typing `=in2mm(A1)` or `=in2mm(10)` into a cell.

To learn more about custom functions, try the
[Menus and Custom Functions](https://developers.google.com/apps-script/quickstart/custom-functions) 5-minute
quickstart, or take a look at the more in-depth
[guide to custom functions](https://developers.google.com/apps-script/guides/sheets/functions).

## Macros

Macros are another way of executing Apps Script code from the
Sheets UI. Unlike custom functions, you activate them with a
keyboard shortcut or through the Sheets menu. For more
information, see [Sheets Macros](https://developers.google.com/apps-script/guides/sheets/macros).

## Add-ons for Google Sheets

[Add-ons](https://developers.google.com/workspace/add-ons/overview) are specially packaged
Apps Script projects that run inside Sheets and
can be installed from the Sheets
add-on store. If you've developed a script for
Sheets and want to share it, Apps Script lets you
[publish](https://developers.google.com/workspace/add-ons/how-tos/editor-publish-overview) your script as an
add-on so other users can install it.

## Performance and scaling

As your datasets grow, you might experience performance issues. To optimize your
spreadsheet and scripts:

- **Follow best practices** : Read the [Best Practices guide](https://developers.google.com/apps-script/guides/support/best-practices) for tips on minimizing service calls and using batch operations.
- **Optimize formulas** : If your spreadsheet is laggy due to complex formulas (like `VLOOKUP`, `ARRAYFORMULA`, or `IMPORTRANGE`), consider using Apps Script to perform these calculations in memory and write the results back in batches.
- **Consider database alternatives** : For very large datasets (approaching 10 million cells) or high-frequency data entry (e.g., many connected forms), consider using [Google Cloud SQL using JDBC](https://developers.google.com/apps-script/guides/jdbc) or [BigQuery](https://developers.google.com/apps-script/advanced/bigquery).

## Triggers

Scripts that are [bound](https://developers.google.com/apps-script/guides/bound) to a Sheets
file can use [simple triggers](https://developers.google.com/apps-script/guides/triggers) like the functions
`onOpen()` and `onEdit()` to respond automatically when a user who has edit
access to the spreadsheet opens or edits the spreadsheet.
Like simple triggers, [installable triggers](https://developers.google.com/apps-script/guides/triggers/installable) let
Sheets run a function automatically when a certain event occurs.
Installable triggers, however, offer more flexibility than simple triggers and
support the following events: open, edit, change, form submit, and time-driven
(clock).


CustomFunctions in Google Sheets
Google Sheets offers hundreds of
[built-in functions](https://support.google.com/drive/topic/1361471) like
[`AVERAGE`](https://support.google.com/drive/answer/3093615),
[`SUM`](https://support.google.com/drive/answer/3093669), and
[`VLOOKUP`](https://support.google.com/drive/answer/3093318). When these aren't
enough for your needs, you can use Apps Script to write custom
functions then use them in Sheets just like a built-in function.

> [!NOTE]
> **Note:** For improved spreadsheet performance, check if your logic can be built using [named functions](https://support.google.com/docs/answer/12504534). They leverage the built-in spreadsheet engine for instant calculations and work seamlessly without requiring script authorization or exceeding daily quotas.

For examples of custom functions, see the following tutorials:

- [Calculate sale price of discounted items (quickstart)](https://developers.google.com/apps-script/quickstart/custom-functions)
- [Calculate a tiered pricing discount](https://developers.google.com/apps-script/samples/custom-functions/tier-pricing)
- [Calculate driving distance \& convert meters to miles](https://developers.google.com/apps-script/samples/custom-functions/calculate-driving-distance)
- [Summarize data from multiple sheets](https://developers.google.com/apps-script/samples/custom-functions/summarize-sheets-data)
- [Fact-check statements with an ADK AI agent and Gemini model](https://developers.google.com/apps-script/samples/custom-functions/fact-check)

## Getting started

Custom functions are created using standard JavaScript. If you're new to
JavaScript, Codecademy offers a
[course for beginners](https://www.codecademy.com/learn/introduction-to-javascript).
This course wasn't developed by and isn't associated with Google.

Here's a custom function, named `DOUBLE`, which multiplies an
input value by 2:

    /**
     * Multiplies an input value by 2.
     * @param {number} input The number to double.
     * @return The input multiplied by 2.
     * @customfunction
    */
    function DOUBLE(input) {
      return input * 2;
    }

If you don't know how to write JavaScript and don't have time to learn,
[check the Google Workspace add-on store](https://developers.google.com/apps-script/guides/sheets/functions#get-a-custom-function) to
see whether someone else has already built the custom function you need.

### Create a custom function

To write a custom function:

1. [Create](https://docs.google.com/spreadsheets/create) or open a spreadsheet in Sheets.
2. Select the menu item **Extensions** \> **Apps Script**.
3. Delete any code in the script editor. For the `DOUBLE` function shown earlier, copy and paste the code into the script editor.
4. At the top, click Save .

Now you can [use the custom function](https://developers.google.com/apps-script/guides/sheets/functions#use-a-custom-function).

### Get a custom function from the Google Workspace Marketplace

The Google Workspace Marketplace offers several custom functions as
[Google Workspace add-ons for
Sheets](https://support.google.com/drive/answer/3641454).
To use or explore these add-ons:

1. [Create](https://docs.google.com/spreadsheets/create) or open a spreadsheet in Sheets.
2. At the top, click **Add-ons \> Get add-ons**.
3. Once the [Google Workspace Marketplace](https://workspace.google.com/marketplace) opens, click the search box in the top right corner.
4. Type "custom function" and press Enter.
5. If you find a custom function add-on you're interested in, click **Install** to install it.
6. A dialog might tell you that the add-on requires authorization. If so, read the notice carefully, then click **Allow**.
7. The add-on becomes available in the spreadsheet. To use the add-on in a different spreadsheet, open the other spreadsheet and at the top, click **Add-ons \> Manage add-ons** . Find the add-on you want to use and click Options \> **Use in this
   document**.

### Use a custom function

Once you've written a custom function or installed one from the
Google Workspace Marketplace, it's used just like a built-in function:

1. Click the cell where you want to use the function.
2. Type an equals sign (`=`) followed by the function name and any input value --- for example, `=DOUBLE(A1)` --- and press Enter.
3. The cell momentarily displays `Loading...`, then returns the result.

## Guidelines for custom functions

Before writing your own custom function, there are a few guidelines to know.

### Function naming

In addition to the standard conventions for naming JavaScript functions, be
aware of the following:

- The name of a custom function must be distinct from the names of [built-in functions](https://support.google.com/docs/table/25273) like `SUM()`.
- The name of a custom function can't end with an underscore (`_`), which denotes a private function in Apps Script.
- The name of a custom function must be declared with the syntax `function myFunction()`, not `var myFunction = new Function()`.
- Capitalization doesn't matter, although the names of spreadsheet functions are traditionally uppercase.

### Arguments

Like a built-in function, a custom function can take arguments as input values:

- If you call your function with a reference to a single cell as an argument (like `=DOUBLE(A1)`), the argument is the value of the cell.
- If you call your function with a reference to a range of cells as an
  argument (like `=DOUBLE(A1:B10)`), the argument is a two-dimensional
  array of the cells' values. For example, in the following screenshot, the
  arguments in `=DOUBLE(A1:B2)` are interpreted by Apps Script as
  `double([[1,3],[2,4]])`. Note that the sample code for `DOUBLE`
  [described earlier](https://developers.google.com/apps-script/guides/sheets/functions#getting-started) would need to be
  [modified to accept an array as input](https://developers.google.com/apps-script/guides/sheets/functions#optimization).

  ![](https://developers.google.com/static/apps-script/images/arguments-example.png)  
- Custom function arguments must be
  [deterministic](http://en.wikipedia.org/wiki/Deterministic_algorithm). That
  is, built-in spreadsheet functions that return a different result each time
  they calculate --- such as `NOW()` or `RAND()` --- are not allowed as arguments
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

- If a custom function returns a value, the value displays in the cell the function was called from.
- If a custom function returns a two-dimensional array of values, the values overflow into adjacent cells as long as those cells are empty. If this would cause the array to overwrite existing cell contents, the custom function throws an error instead. For an example, see the section on [optimizing custom functions](https://developers.google.com/apps-script/guides/sheets/functions#optimization).
- A custom function can't affect cells other than those it returns a value to. In other words, a custom function can't edit arbitrary cells, only the cells it is called from and their adjacent cells. To edit arbitrary cells, use a [custom menu](https://developers.google.com/apps-script/guides/menus) to run a function instead.
- A custom function call must return within 30 seconds. If it doesn't, the cell displays `#ERROR!` and the cell note is `Exceeded maximum execution time
  (line 0).`

### Data types

Sheets stores data in
[different formats](https://support.google.com/docs/answer/56470) depending on
the nature of the data. When these values are used in custom functions,
Apps Script treats them as the
[appropriate data type in JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures).
These are the most common areas of confusion:

- Times and dates in Sheets become [Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) objects in Apps Script. If the spreadsheet and the script use different time zones (a rare problem), the custom function needs to compensate.
- Duration values in Sheets also become `Date` objects, but [working with them can be complicated](http://stackoverflow.com/questions/17715841/gas-how-to-read-the-correct-time-values-form-google-spreadsheet).
- Percentage values in Sheets become decimal numbers in Apps Script. For example, a cell with a value of `10%` becomes `0.1` in Apps Script.

### Autocomplete

Sheets supports autocomplete for custom functions much like for
[built-in functions](https://support.google.com/docs/answer/91932). As you
type a function name in a cell, you see a list of built-in and custom
functions that matches what you enter.

Custom functions appear in this list if their script includes a
[JSDoc](https://developers.google.com/apps-script/concepts/jsdoc) `@customfunction` tag, as in the `DOUBLE()`
example.

> [!NOTE]
> **Note:** While Apps Script supports standard JSDoc for autocomplete in the editor, the Google Sheets UI has [specific limitations](https://developers.google.com/apps-script/concepts/jsdoc#supported_tags_and_ui_limitations) regarding which tags and syntax are displayed in the spreadsheet's formula helper.

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

| Supported services | Notes |
|---|---|
| [Cache](https://developers.google.com/apps-script/reference/cache) | Works, but not particularly useful in custom functions |
| [HTML](https://developers.google.com/apps-script/reference/html) | Can generate HTML, but can't display it (rarely useful) |
| [JDBC](https://developers.google.com/apps-script/reference/jdbc) |   |
| [Language](https://developers.google.com/apps-script/reference/language) |   |
| [Lock](https://developers.google.com/apps-script/reference/lock) | Works, but not particularly useful in custom functions |
| [Maps](https://developers.google.com/apps-script/reference/maps) | Can calculate directions, but not display maps |
| [Properties](https://developers.google.com/apps-script/reference/properties) | `getUserProperties()` only gets the properties of the spreadsheet owner. Spreadsheet editors can't set user properties in a custom function. |
| [Spreadsheet](https://developers.google.com/apps-script/reference/spreadsheet) | Read-only (can use most `get*()` methods, but not `set*()`). Cannot open other spreadsheets (`SpreadsheetApp.openById()` or `SpreadsheetApp.openByUrl()`). |
| [URL Fetch](https://developers.google.com/apps-script/reference/url-fetch) | Access resources on the web by fetching URLs. |
| [Utilities](https://developers.google.com/apps-script/reference/utilities) |   |
| [XML](https://developers.google.com/apps-script/reference/xml-service) |   |

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

- Click **Extensions** \> **Apps Script** to open the script editor, then copy the script text from the original spreadsheet and paste it into the script editor of another spreadsheet.
- Make a copy of the spreadsheet that contains the custom function by clicking **File \> Make a copy**. When a spreadsheet is copied, any scripts attached to it are copied as well. Anyone who has access to the spreadsheet can copy the script. (Collaborators who have only view access can't open the script editor in the original spreadsheet. However, when they make a copy, they become the owner of the copy and can see the script.)
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

These techniques can be applied to nearly any custom function that is used
repeatedly throughout a spreadsheet, although the implementation details vary
depending on the function's behavior.


# Google Sheets Macros

Google Sheets lets you record
[macros](https://support.google.com/docs/answer/7665004) that duplicate a
specific series of UI interactions that you define. Once you've recorded a
macro, you can link it to a keyboard shortcut in the form
`Ctrl+Alt+Shift+Number`. Use that shortcut to quickly execute the
exact macro steps again, typically in a different place or on different data.
You can also activate the macro from the Sheets **Extensions**
\> **Macros** menu.

When you record a macro, Sheets automatically creates an
Apps Script function (the *macro function* ) that replicates the
macro steps. The macro function is added to an Apps Script
project [bound](https://developers.google.com/apps-script/guides/bound) to the sheet, in a file titled
`macros.gs`. In the event that there is already a project file bound to the
sheet with that name, the macro function is appended to it.
Sheets also automatically updates the script project
[manifest](https://developers.google.com/apps-script/concepts/manifests), recording the name and keyboard
shortcut assigned to the macro.

Since every recorded macro is defined entirely within
Apps Script, you can edit them directly within the
Apps Script editor. You can even write macros from scratch in
Apps Script, or take functions you've already written and turn
them into macros.

## Create macros in Apps Script

You can take functions written in Apps Script and use them as
macro functions. A straightforward way to do this is by [importing an existing
function](https://developers.google.com/apps-script/guides/sheets/macros#import-functions-as-macros) from the Sheets editor.

Alternatively, you can create macros within the Apps Script
editor by following these steps:

1. In the Sheets UI, select **Extensions** \> **Apps Script** to open the script bound to the sheet in the Apps Script editor.
2. Write the macro function. Macro functions should take no arguments and return no values.
3. Edit your [script manifest](https://developers.google.com/apps-script/concepts/manifests#editing_a_manifest) to create the macro and link it to the macro function. Assign it a unique keyboard shortcut and name.
4. Save the script project. The macro is then available for use in the sheet.
5. Test the macro function in the sheet to verify that functions as intended.

## Edit macros

To edit macros attached to a sheet, do the following:

1. In the Sheets UI, select **Extensions** \> **Macros** \> **Manage macros**.
2. Find the macro you want to edit and select **\> Edit macro**. This opens the Apps Script editor to the project file containing the macro function.
3. Edit the macro function to change the macro behavior.
4. Save the script project. The macro is then available for use in the sheet.
5. Test the macro function in the sheet to verify that functions as intended.

## Import functions as macros

If there is already a script [bound](https://developers.google.com/apps-script/guides/bound) to a sheet,
you can *import* a function in the script as a new macro and then assign it
a keyboard shortcut. Do this by
[editing the manifest](https://developers.google.com/apps-script/concepts/manifests#editing_a_manifest)
file and adding another element to the
[`sheets.macros[]`](https://developers.google.com/apps-script/guides/sheets/macros#manifest-structure-for-macros) property.

Alternatively, follow these steps to import a function as a macro from the
Sheets UI:

1. In the Sheets UI, select **Extensions** \> **Macros** \> **Import**.
2. Select a function from the list presented and then click **Add function**.
3. Select to close the dialog.
4. Select **Extensions** \> **Macros** \> **Manage macros**.
5. Locate the function you just imported in the list. Assign a unique keyboard shortcut to the macro. You can also change the macro name here; the name defaults to the name of the function.
6. Click **Update** to save the macro configuration.

## Manifest structure for macros

The following manifest file example snippet shows the section of a
[manifest](https://developers.google.com/apps-script/concepts/manifests) that defines Sheets
macros.
The `sheets` section of the manifest defines the name and keyboard shortcut
assigned to the macro and the name of the macro function.

Manifests include other components that relate to Apps Script
properties. The fields under the `sheets` key relate directly to
Sheets functionality. This example is just a portion of a full
manifest file and is not a fully functional manifest.

    {
      ...
      "sheets": {
        "macros": [{
          "menuName": "QuickRowSum",
          "functionName": "calculateRowSum",
          "defaultShortcut": "Ctrl+Alt+Shift+1"
        }, {
          "menuName": "Headerfy",
          "functionName": "updateToHeaderStyle",
          "defaultShortcut": "Ctrl+Alt+Shift+2"
        }]
      }
    }

See the [Sheets macro manifest resource](https://developers.google.com/apps-script/manifest/sheets)
for more details on how Sheets macro manifests are constructed.

## Best practices

When creating or managing macros in Apps Script, follow these guidelines:

1. Macros are more performant when they are lightweight. Where possible, limit the number of actions a macro takes.
2. Macros are best suited for rote operations that need to be repeated frequently with little or no configuration. For other operations, consider using a [custom menu item](https://developers.google.com/apps-script/guides/menus) instead.
3. Always remember that macro keyboard shortcuts must be unique, and a given sheet can only have ten macros with shortcuts at any one time. Any additional macros can only be executed from the **Extensions** \> **Macros** menu.
4. Macros that make changes to a single cell can be applied to a range of cells by first selecting the full range and then activating the macro. This means it is often unnecessary to create macros that duplicate the same operation across a predefined range of cells.

## Things you can't do

There are a few restrictions on what you can do with macros:

#### NoUse macros outside bound scripts

Macros are defined in scripts bound to specific Sheets. Macro
definitions are ignored if defined in a
[standalone script](https://developers.google.com/apps-script/guides/standalone) or
[web app](https://developers.google.com/apps-script/guides/web).

#### NoDefine macros in Sheets Google Workspace add-ons

You cannot distribute macro definitions using a
[Sheets Google Workspace add-on](https://developers.google.com/workspace/add-ons/overview).
Any macro definitions in a Sheets
add-on project are ignored by users of that
add-on.

#### NoDistribute macros in script libraries

You cannot distribute macro definitions using Apps Script
[libraries](https://developers.google.com/apps-script/guides/libraries).

#### NoUse macros outside of Sheets

Macros are only a feature in Sheets, and don't exist for
Google Docs, Forms, or Google Slides.

# Use Connected Sheets

[Connected Sheets](https://cloud.google.com/blog/products/g-suite/connected-sheets-is-generally-available)
is a Google Sheets feature that lets you analyze BigQuery and Looker
data directly within Sheets. Access
Connected Sheets programmatically with the Spreadsheet service.

## Common Connected Sheets actions

Use the `DataSource` classes and objects to connect to BigQuery or Looker and
analyze data.
The following table lists the most common `DataSource` actions and
how to create them in Google Apps Script:

| Action | Apps Script class | Method to use |
|---|---|---|
| Connect a sheet to a supported data source | [`DataSourceSpec`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-spec) | `SpreadsheetApp.newDataSourceSpec()` |
| Choose a data source | [`DataSource`](https://developers.google.com/apps-script/reference/spreadsheet/data-source) | `Spreadsheet.insertDataSourceSheet().getDataSource()` |
| Add a data source sheet | [`DataSourceSheet`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-sheet) | `Spreadsheet.insertDataSourceSheet()` |
| Add a pivot table | [`DataSourcePivotTable`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-pivot-table) | `Range.insertDataSourcePivotTable()` |
| Pull data into an extract | [`DataSourceTable`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-table) | `Range.insertDataSourceTable()` |
| Use a formula | [`DataSourceFormula`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-formula) | `Range.setFormula()` |
| Add a chart | [`DataSourceChart`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-chart) | `Sheet.insertDataSourceChart()` |

## Add required authorization scopes

To access BigQuery data, include the `enableBigQueryExecution()` method
in your Apps Script code. This method adds the required
`bigquery.readonly` OAuth scope to your Apps Script project.

The following sample shows the `SpreadsheetApp.enableBigQueryExecution()` method
called within a function:

    function addDataSource() {
      SpreadsheetApp.enableBigQueryExecution();
      var spreadsheet = SpreadsheetApp.getActive();
      }

To access Looker data, include the `enableLookerExecution()` method in
your Apps Script code. Accessing Looker in
Apps Script reuses your existing Google Account Link with Looker.

The following sample shows the `SpreadsheetApp.enableLookerExecution()` method
called within a function:

    function addDataSource() {
      SpreadsheetApp.enableLookerExecution();
      var spreadsheet = SpreadsheetApp.getActive();
      }

### Add additional OAuth scopes to the manifest file

When connecting with BigQuery, most OAuth scopes are automatically added to the
manifest file based on the functions used in your code. If you need additional
scopes to access certain BigQuery data, you can
[set explicit scopes](https://developers.google.com/apps-script/concepts/scopes#setting_explicit_scopes).

For example, to [query BigQuery data hosted within
Google Drive](https://cloud.google.com/bigquery/external-data-drive#api),
you must add a Drive OAuth scope to your manifest file.

The following sample shows the `oauthScopes` portion of a manifest file. It adds
a Drive OAuth scope in addition to the minimum required
`spreadsheet` and `bigquery.readonly` OAuth scopes:

    { ...
      "oauthScopes": [
        "https://www.googleapis.com/auth/bigquery.readonly",
        "https://www.googleapis.com/auth/spreadsheets",
        "https://www.googleapis.com/auth/drive" ],
    ... }

## Example: Create and refresh a data source object

The following examples shows how to add a data source, create a data
source object from the data source, refresh the data source object, and get
the execution status.

### Add a data source

The following examples show how to add a BigQuery and a Looker data source
respectively.

#### BigQuery

To add a BigQuery data source to a spreadsheet, insert a data source sheet with
a data source spec. The data source sheet is automatically refreshed to fetch
preview data.

Replace `<YOUR_PROJECT_ID>` below with a valid Google Cloud project ID.

    // For operations that fetch data from BigQuery, enableBigQueryExecution() must be called.
    SpreadsheetApp.enableBigQueryExecution();
    var spreadsheet = SpreadsheetApp.create('Test connected sheets');
    Logger.log('New test spreadsheet: %s', spreadsheet.getUrl());

    // Build data source spec by selecting a table.
    var dataSourceSpec = SpreadsheetApp.newDataSourceSpec()
        .asBigQuery()
        .setProjectId('<YOUR_PROJECT_ID>')
        .setTableProjectId('bigquery-public-data')
        .setDatasetId('ncaa_basketball')
        .setTableId('mbb_historical_tournament_games')
        .build();
    // Add data source and its associated data source sheet.
    var dataSourceSheet = spreadsheet.insertDataSourceSheet(dataSourceSpec);
    var dataSource = dataSourceSheet.getDataSource();

#### Looker

To add a Looker data source to a spreadsheet, insert a data source sheet with a
data source spec. The data source sheet is automatically refreshed to fetch
preview data.

Replace `<INSTANCE_URL>`,`<MODEL_NAME>`, `<EXPLORE_NAME>` in the following
sample with a valid Looker instance URL, model name and explore name
respectively.

    // For operations that fetch data from Looker, enableLookerExecution() must be called.
    SpreadsheetApp.enableLookerExecution();
    var spreadsheet = SpreadsheetApp.create('Test connected sheets');
    Logger.log('New test spreadsheet: %s', spreadsheet.getUrl());

    // Build data source spec by selecting a table.
    var dataSourceSpec = SpreadsheetApp.newDataSourceSpec()
        .asLooker()
        .setInstanceUrl('<INSTANCE_URL>')
        .setModelName('<MODEL_NAME>')
        .setExploreName('<EXPLORE_NAME>')
        .build();
    // Add data source and its associated data source sheet.
    var dataSourceSheet = spreadsheet.insertDataSourceSheet(dataSourceSpec);
    var dataSource = dataSourceSheet.getDataSource();

### Add a data source object

Once the data source is added to the spreadsheet, data source objects can be
created from the data source. In this example, a pivot table is created using
`DataSourcePivotTable` on the BigQuery `dataSource` created in
[the code sample which adds a BigQuery data source](https://developers.google.com/apps-script/guides/sheets/connected-sheets#adding-a-bigquery-data-source).

Unlike regular data in grid sheets that are referenced by cell index or A1
notations, data from data sources are usually referenced by column names.
Therefore, most property setters on data source objects use column name as
input.

    var rootCell = spreadsheet.insertSheet('pivotTableSheet').getRange('A1');

    // Add data source pivot table and set data source specific configurations.
    var dataSourcePivotTable = rootCell.createDataSourcePivotTable(dataSource);
    var rowGroup = dataSourcePivotTable.addRowGroup('season');
    rowGroup.sortDescending().setGroupLimit(5);
    dataSourcePivotTable.addColumnGroup('win_school_ncaa');
    dataSourcePivotTable.addPivotValue('win_pts',
    SpreadsheetApp.PivotTableSummarizeFunction.AVERAGE);
    dataSourcePivotTable.addPivotValue('game_date',
    SpreadsheetApp.PivotTableSummarizeFunction.COUNTA);
    var filterCriteria = SpreadsheetApp.newFilterCriteria()
        .whenTextEqualToAny(['Duke', 'North Carolina'])
        .build();
    dataSourcePivotTable.addFilter('win_school_ncaa', filterCriteria);

    // Get a regular pivot table instance and set shared configurations.
    var pivotTable = dataSourcePivotTable.asPivotTable();
    pivotTable.setValuesDisplayOrientation(SpreadsheetApp.Dimension.ROWS);

### Refresh a data source object

Refresh data source objects to fetch the latest data from BigQuery
based on the data source specs and object configurations.

The process to refresh data is asynchronous. To refresh a data source object,
use the following methods:

1. `refreshData()` starts the data refresh execution.
2. `waitForCompletion()` returns the end state once the data execution is completed. This eliminates the need to keep polling the execution status.
3. `DataExecutionStatus.getErrorCode()` gets the error code in case the data execution fails.

The following sample illustrates a refresh of the pivot table data:

    var status = dataSourcePivotTable.getStatus();
    Logger.log('Initial state: %s', status.getExecutionState());

    dataSourcePivotTable.refreshData();

    status = dataSourcePivotTable.waitForCompletion(/* timeoutInSeconds= */ 60);
    Logger.log('Ending state: %s', status.getExecutionState());
    if (status.getExecutionState() == SpreadsheetApp.DataExecutionState.ERROR) {
      Logger.log('Error: %s (%s)', status.getErrorCode(),
      status.getErrorMessage());
    }

## Use triggers with Connected Sheets

Automate your Connected Sheets data source functions with
[triggers and events](https://developers.google.com/apps-script/guides/triggers/installable).
For example, use
[time-driven triggers](https://developers.google.com/apps-script/guides/triggers/installable#time-driven_triggers)
to refresh data source objects repeatedly at a specific time, and use
spreadsheet
[event triggers](https://developers.google.com/apps-script/guides/triggers/installable#g_suite_application_triggers)
to trigger data execution on a predefined event.

The following sample adds a BigQuery data source with a query parameter and
refreshes the data source sheet when the query parameter is edited.

Replace `<YOUR_PROJECT_ID>` with a valid Google Cloud project ID.

    // Add data source with query parameter.
    function addDataSource() {
      SpreadsheetApp.enableBigQueryExecution();
      var spreadsheet = SpreadsheetApp.getActive();

      // Add a new sheet and use A1 cell as the parameter cell.
      var parameterCell = spreadsheet.insertSheet('parameterSheet').getRange('A1');
      parameterCell.setValue('Duke');

      // Add data source with query parameter.
      var dataSourceSpec = SpreadsheetApp.newDataSourceSpec()
          .asBigQuery()
          .setProjectId('<YOUR_PROJECT_ID>')
          .setRawQuery('select * from `bigquery-public-data`.`ncaa_basketball`.`mbb_historical_tournament_games` WHERE win_school_ncaa = @SCHOOL')
          .setParameterFromCell('SCHOOL', 'parameterSheet!A1')
          .build();
      var dataSourceSheet = spreadsheet.insertDataSourceSheet(dataSourceSpec);
      dataSourceSheet.asSheet().setName('ncaa_data');
    }

    // Function used to configure event trigger to refresh data source sheet.
    function refreshOnParameterEdit(e) {
      var editedRange = e.range;
      if (editedRange.getSheet().getName() != 'parameterSheet') {
        return;
      }
      // Check that the edited range includes A1.
      if (editedRange.getRow() > 1 || editedRange.getColumn() > 1) {
         return;
      }

      var spreadsheet = e.source;
      SpreadsheetApp.enableBigQueryExecution();
      spreadsheet.getSheetByName('ncaa_data').asDataSourceSheet().refreshData();
    }

In the preceding sample, the `addDataSource()` function adds a data source to
the spreadsheet. After you execute `addDataSource()`, create an event trigger in
the Apps Script editor. To learn how to create an event trigger,
see [Installable triggers](https://developers.google.com/apps-script/guides/triggers/installable).

Select the following options for your trigger:

- **Event source** : **From spreadsheet**
- **Event type** : **On edit**
- **Function to run** : **`refreshOnParameterEdit`**

Once the trigger is created, the data source sheet refreshes automatically
every time the parameter cell is edited.

## Troubleshoot

| Error message | Resolution |
|---|---|
| Use `enableBigQuery()` to enable data executions for BIGQUERY data sources. | This error indicates that `SpreadsheetApp.enableBigQueryExecution()` is not called before fetching BigQuery data. Call `SpreadsheetApp.enableBigQueryExecution()` in functions that use methods for BigQuery execution. Such as, `refreshData()` on data source objects, `Spreadsheet.insertDataSourceTable()`, and `DataSource.updateSpec()`. These methods require an additional bigquery.readonly OAuth scope to work. |
| Not permitted to act on data sources. Please contact your administrator to enable the feature. | This error indicates that the account doesn't have Connected Sheets enabled. Connected Sheets is only available to Google Workspace users with certain subscriptions. Contact your administrator to enable the feature. |