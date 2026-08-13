# Libraries

A library is a script project whose functions can be reused in other scripts.

A script that uses a library
[doesn't run as quickly](https://developers.google.com/apps-script/guides/support/best-practices#avoid_libraries_in_ui-heavy_scripts)
as it would if all the code were contained within a single script project.
Although libraries can make development and maintenance more convenient, use
them sparingly in projects where speed is critical. Because of this
issue, library use should be limited in [Google Workspace add-ons](https://developers.google.com/workspace/add-ons/overview).

## Gain access to a library

To include a library in your project you must have at least view-level
access to it. If you aren't the author of the library that you want to
include, contact the author and request access.

You need the script ID of the library you want to include. When you have
access to the library, find the script ID on the **Project Settings**
page.

## Add a library to your script project

1. At the left of the Apps Script editor, next to "Libraries," click Add a library .
2. In the "Script ID" field, paste in the script ID of the library.
3. Click **Look up** .

   > [!NOTE]
   > If you encounter an error, make sure that you have at least view-level access to the project that you're trying to include.

4. Click the **Version** drop-down and select the version of the library to use.
5. Check to see if the default "Identifier" name is the one that you want to use with this library. This is the name that your script uses to refer to the library. For example, if you set it to `Test` then call a method of that library as follows: `Test.libraryMethod`.

   > [!CAUTION]
   > If you use an identifier name that matches the name of an already existing service, such as [`MailApp`](https://developers.google.com/apps-script/reference/mail/mail-app), or a previously added library, then the library you have added most recently overrides the existing service or library.

6. Click **Add**.

## Use a library

Use your included library as you would use a default service. For
example, if `Test` is the identifier for your library, type
`Test` immediately followed by a period to see the list of methods in the
library.

Open the reference documentation for an included library by following these
steps:

At the left of the script editor, next to the library name, click More
**\> Open in a new tab**.

## Remove a library

At the left of the script editor, next to the library name, click More
**\> Remove \> Remove library**.

If a library is deleted by the author you still need to remove it from your
list of included libraries.

## Update a library

Change the version of the library or update its identifier.

1. At the left of the editor, under "Libraries," click the name of the library.
2. Make your changes and click **Save**.

## Create and share a library

To use and share your script project as a library, follow these steps:

1. [Create a versioned deployment](https://developers.google.com/apps-script/guides/versions) of your script.
2. Share at least view-level access with all potential users of the library.
3. Give those users the script ID, which can be found on the **Project
   Settings** page.

### Best practices

Here are some guidelines to follow when writing a library:

1. Choose a meaningful name for your project since it's used as the default identifier when your library is included by others.
2. To make one or more methods of your script not be visible (nor usable) to your library users, end the name of the method with an underscore. For example, `myPrivateMethod_`.
3. Only enumerable global properties are visible to library users. This includes function declarations, variables created outside a function with `var`, and properties explicitly set on the global object. For example, `Object.defineProperty()` with `enumerable` set to `false` creates a symbol you can use in your library, but this symbol isn't accessible by your users.
4. To ensure your library users can make use of the script editor autocomplete
   and the automatically generated documentation, include JSDoc-style
   documentation for all your functions. Here's an example:

       /**
        * Raises a number to the given power, and returns the result.
        *
        * @param {number} base the number we're raising to a power
        * @param {number} exp the exponent we're raising the base to
        * @return {number} the result of the exponential calculation
        */
       function power(base, exp) { ... }

### Resource scoping

There are two types of resources when you are working with libraries: shared
and not-shared. A shared resource means that both the library and the including
script have a built-in access to the same instance of the resource. The
following diagram illustrates a shared resource using the example of
User Properties:

![Shared Resource](https://developers.google.com/static/apps-script/images/includes_shared_diagram.png)

A not-shared resource means that both library and the including script have
built-in access only to their instance of the resource. However, a library can
provide access to its not-shared resources by having explicit functions that
operate on them. Here is an example of a function that you would include in
your library to expose its Script Properties:

      function getLibraryProperty(key) {
        const scriptProperties = PropertiesService.getScriptProperties();
        return scriptProperties.getProperty(key);
      }

The following diagram illustrates a not-shared resource using the example of
Script Properties:

![Example of a not-shared resource](https://developers.google.com/static/apps-script/images/includes_not_shared_diagram.png)

This table lists the shared and not-shared resources for your reference:

| Resource | Shared\* | Not-Shared\*\* | Notes |
|---|---|---|---|
| Lock |   | ![](https://developers.google.com/static/apps-script/images/check.svg) | The same instance is visible to all including scripts when created in the library. |
| Script Properties |   | ![](https://developers.google.com/static/apps-script/images/check.svg) | The same instance is visible to all including scripts when created in the library. |
| Cache |   | ![](https://developers.google.com/static/apps-script/images/check.svg) | The same instance is visible to all including scripts when created in the library. |
| Triggers |   | ![](https://developers.google.com/static/apps-script/images/check.svg) | Simple triggers created in library are not triggered by the including script. |
| ScriptApp | ![](https://developers.google.com/static/apps-script/images/check.svg) |   |   |
| UiApp | ![](https://developers.google.com/static/apps-script/images/check.svg) |   |   |
| User Properties | ![](https://developers.google.com/static/apps-script/images/check.svg) |   |   |
| Logger and execution transcript | ![](https://developers.google.com/static/apps-script/images/check.svg) |   |   |
| Sites, Sheets and other containers | ![](https://developers.google.com/static/apps-script/images/check.svg) |   | A call to `getActive` returns the container of the including script. |
| MailApp and GmailApp | ![](https://developers.google.com/static/apps-script/images/check.svg) |   |   |

## Test a library

To test your library, use the head deployment. Anyone who has editor-level
access to the script can use the head deployment.

You still need at least one version of the library saved.

## Debug a library

When you debug a script that includes a library, you can't step into the library code or set breakpoints in it. If you try to step into a library function in debug mode, the debugger skips the function and steps to the next line in the calling script.

Using **HEAD (Development Mode)** for the library version doesn't enable stepping into the library or hitting breakpoints within it.

To debug library code, use one of the following methods:

- **Debug from the library project**: Open the library script project in the Apps Script editor. To test library functions with specific arguments, create a temporary "test" function within the library project that calls your library functions, then run that test function in debug mode.
- **Logging** : Use `console.log()` within your library functions to output information to the execution logs. When the library is called by another script, these logs appear in the [execution logs](https://developers.google.com/apps-script/guides/logging#execution_log_logging) of the calling script.