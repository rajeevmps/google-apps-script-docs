# Extend Google Sheets with add-ons

### Page Summary

- Google Sheets add-ons enhance spreadsheets with custom workflows, external system connections, and integration with other Google Workspace apps.
- Add-ons, built using Apps Script, enable data manipulation, custom menus, dialogs, and functions, triggered by specific events.
- Custom functions extend Google Sheets' built-in formulas, accessible directly within cells, but require adherence to naming and usage guidelines.
- Google Sheet add-ons provide extended functionality but cannot currently distribute or utilize pre-recorded macros.

### Introduction

Google Sheets is a cloud-based spreadsheet solution with real-time collaboration and powerful tools to visualize, process and communicate data.

You can extend Sheets with add-ons that build customized workflow improvements, establish connectivity to third-party systems, and integrate your Sheets data with other Google Workspace applications (like Google Slides).

You can see the Sheets add-ons others have built on the [Google Workspace Marketplace](https://workspace.google.com/marketplace/category/works-with-spreadsheet).

### What you can do

Here are a few things you can do with add-ons that extend Sheets:

- Read, edit, visualize, and format data in Sheets spreadsheets using the built-in Apps Script [Spreadsheet service](/apps-script/reference/spreadsheet). The service also lets you create and modify conditional formatting and data validation rules.
- Use the Apps Script [advanced Sheets service](/apps-script/advanced/sheets) to access the [Google Sheets API](/workspace/sheets/api) directly.
- Create [custom menus](/workspace/add-ons/concepts/menus) and define multiple [custom dialogs and sidebars](/workspace/add-ons/concepts/dialogs) interfaces using standard HTML and CSS.
- Include [custom function](#custom_functions) definitions in your add-on.
- Use add-ons [triggers](#triggers) that run specified functions when certain triggering events occur.

Sheets add-ons are built using Apps Script. To learn more about how to access and manage Sheets with Apps Script, see [Extend Sheets](/apps-script/guides/sheets).

### Sheet structure

A Sheets spreadsheet consists of one or more sheets. Each sheet is essentially a 2D grid of cells into which text, numbers, links, or other values can be stored. A group of one or more adjacent cells is called a _range_.

The Apps Script [Spreadsheet service](/apps-script/reference/spreadsheet) provides several classes to represent organizational structures in Sheets (such as [`Sheet`](/apps-script/reference/spreadsheet/sheet) and [`Range`](/apps-script/reference/spreadsheet/range)). You can use these classes to read and modify Sheets data and behavior.

### Triggers

Apps Script [triggers](/workspace/add-ons/concepts/editor-triggers) let a script project execute a specified function when certain conditions are met, such as when a spreadsheet is opened or when an add-on is installed.

See [add-on triggers](/workspace/add-ons/concepts/editor-triggers) for more information on what triggers can be used with Sheets add-ons and what restrictions apply to their use.

### Custom functions

Sheets has a number of [built-in functions](https://support.google.com/docs/table/25273?ref_topic=1361471) like `SUM` and `AVERAGE` that can be invoked from within a Sheets cell. Sheets add-ons can define additional [custom functions](/apps-script/guides/sheets/functions) to supplement these built-in functions. When a user installs the add-on, any defined custom functions included with the add-on become available immediately. It is possible for an add-on to consist of only custom function definitions. Custom function definitions are primarily shared with others by publishing an add-on containing the definitions.

#### Create add-on custom functions

Any function defined in an add-on script project can be used as a custom function. Once the function is implemented and the add-on is installed, you can call the custom function like any other built-in Sheets function: in a Sheet cell, enter the `=` followed by the name of the function and any required parameters. If there are no errors, the result returned by the function is placed in the Sheets cell, overflowing to neighboring cells as necessary.

When creating custom functions in an add-on you should follow the general custom function guidelines:

- [Function naming guidelines](/apps-script/guides/sheets/functions#naming)
- [Defining function arguments](/apps-script/guides/sheets/functions#arguments)
- [Defining the function return value](/apps-script/guides/sheets/functions#return_values)
- [Custom function data types](/apps-script/guides/sheets/functions#data_types)
- [Enabling autocomplete using JSDoc](/apps-script/guides/sheets/functions#autocomplete)
- [Services custom functions can use](/apps-script/guides/sheets/functions#using_apps_script_services)
- [Optimizing custom functions](/apps-script/guides/sheets/functions#optimization)

In addition, custom functions defined in add-ons have some special considerations:

- When naming your function, try to create a unique name, perhaps related to the name of your add-on. If two or more installed add-ons define custom functions with the same name, users can only use one of them.
- Your add-on should clearly communicate what custom functions it provides. Be sure to provide accurate JSDoc comments for your custom functions so that Apps Script can present [autocomplete](/apps-script/guides/sheets/functions#autocomplete) information to the user. In addition, consider providing additional documentation of the custom functions either in the add-on itself or on an add-on support web page.
- Custom functions that don't complete in under 30 seconds fail with an `Internal error executing the custom function` error. Build a good user experience by limiting the amount of processing you do in a custom function. [Optimize](/apps-script/guides/sheets/functions#optimization) the function where you can.
- Custom functions can't use Apps Script services that require authorization, and fail with a `You do not have permission to call X service` error if this is attempted. Only use the [permitted services](/apps-script/guides/sheets/functions#using_apps_script_services) in your custom function.
- Each custom function in a Sheets results in a separate call to the Apps Script servers. If a user attempts to use custom functions in too many cells, the functions can execute slowly. To mitigate this, keep your custom functions as straightforward as possible. If you need the function to perform complex or extended processing, don't use a custom function—provide that functionality using a menu item, dialog, or sidebar interaction instead.

### Sheets macros

[Macros](https://support.google.com/docs/answer/7665004) let you record actions taken in Sheets and repeat them later with a keyboard shortcut. When a macro is created in a Sheets, it is added as a _macro function_ in an Apps Script project [bound](/apps-script/guides/bound) to that Sheets. For more information about macros, see [Sheets macros](/apps-script/guides/sheets/macros).

Unfortunately, Sheets macros _can't_ be distributed with add-ons. If you include a macro definition in an add-on's manifest, it is unavailable to users of that add-on.
