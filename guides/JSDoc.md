# JSDoc in Apps Script

documentation in the Google Sheets UI, and script-level annotations.

Google Apps Script uses [JSDoc](https://jsdoc.app/) to generate documentation and
autocomplete for your scripts. JSDoc is a standard for documenting JavaScript
code using comments.

In Apps Script, JSDoc serves these main purposes:

1. **Autocomplete in the editor**: Providing parameter hints and function descriptions as you type.
2. **Custom functions in Google Sheets**: Documenting your custom functions so they appear in the Sheets formula helper.
3. **Script-level annotations**: Using special tags to control script-wide behavior, such as authorization.

## Document functions

To document a function, place a JSDoc comment block directly above the function
declaration. A JSDoc comment starts with `/**` and ends with `*/`.

    /**
     * Multiplies an input value by 2.
     *
     * @param {number} input The value to multiply.
     * @return {number} The input multiplied by 2.
     */
    function double(input) {
      return input * 2;
    }

When you document a function in this way, the Apps Script editor shows a
documentation tooltip when you reference the function. For example, when you
type `double(` in the editor, you see:
> **double(input)**
>
> Multiplies an input value by 2.
>
> **input**: number --- The value to multiply.

### Common tags

| Tag | Description |
|---|---|
| `@param {type} name description` | Documents a function parameter. The `{type}` and `description` are used by the development environment for autocomplete. |
| `@return {type} description` | Documents the function's return value. |
| `@example` | Provides an example of how to use the function. |

### Overloads and multiple types

While JavaScript doesn't support classical function overloading (defining multiple
functions with the same name), you can write a single function that handles
different types of input. You can document these "overloaded" behaviors in JSDoc.

#### Union types

If a parameter or return value can be one of several types, use a pipe (`|`) to
create a union type. This is common in Apps Script for functions that can
accept either a single value or a range of values (represented as a 2D array).

    /**
     * Multiplies an input value (or a range of values) by 2.
     *
     * @param {number|number[][]} input The value or 2D array to multiply.
     * @return {number|number[][]} The result.
     */
    function double(input) {
      return Array.isArray(input) ?
          input.map(row => row.map(cell => cell * 2)) :
          input * 2;
    }

#### Multiple signatures with `@overload`

For functions with complex signatures where the permitted parameters depend on
one another, you can use the `@overload` tag to define each distinct signature.
The Apps Script editor uses these to provide specific hints based on which
version of the function you are calling.

    /**
     * @overload
     * @param {string} name The name of the property to get.
     * @return {string} The property value.
     */
    /**
     * @overload
     * @param {number} index The index of the item to get.
     * @return {object} The item object.
     */
    function get(arg) {
      // Implementation that handles both cases
    }

## Custom functions in Google Sheets

When you write a [custom function](https://developers.google.com/apps-script/guides/sheets/functions) for
Google Sheets, you must use the `@customfunction` tag for it to appear in the
spreadsheet's autocomplete and formula helper.

JSDoc is the source for the helper text that users see when they use your custom
function in Google Sheets. Without JSDoc, users would only see the function
name, making it difficult to know what the function does or what parameters it
requires.

### Supported tags and UI limitations

While Apps Script parses most standard JSDoc tags, the Google Sheets UI for
custom functions has some specific behaviors and limitations:

- **`@customfunction`**: Required for the function to show up in the Sheets formula list.
- **`@param`**: The name and description are displayed in the Sheets formula helper.
- **`@return`** : The description provided in the `@return` tag is **not** displayed in the Sheets formula helper.
- **Optional parameters** : Standard JSDoc syntax for optional parameters (e.g., `[name]` or `name=`) is not recognized by the Sheets UI. All parameters will appear as required in the formula helper.
- **Default values** : Default parameter values (e.g., `[name=Value]`) are not supported in the Sheets UI.
- **Formatting**: HTML tags and plain text line breaks in your description are not supported. The Sheets UI displays the description as a single block of text and strips most HTML.

### Example for Google Sheets

    /**
     * Calculates a discount.
     *
     * @param {number} price The original price.
     * @param {number} percent The discount percentage (e.g., 0.1 for 10%).
     * @return {number} The price after discount.
     * @customfunction
     */
    function calculateDiscount(price, percent) {
      return price * (1 - percent);
    }

#### What users see in Google Sheets

When a user types `=CALCULATEDISCOUNT(` in a cell, Google Sheets displays the
following helper box:
> **CALCULATEDISCOUNT**
>
> Calculates a discount.
>
> **price**: The original price.
>
> **percent**: The discount percentage (e.g., 0.1 for 10%).

Notice that the descriptions for the parameters come directly from your JSDoc
`@param` tags.

## Script-level annotations

Apps Script uses unique JSDoc tags to control script-wide settings. These are
typically placed at the top of a script file.

### Authorization tags

| Tag | Description |
|---|---|
| `@OnlyCurrentDoc` | Tells Apps Script to only request authorization for the current document rather than all files of that type. See the \[Authorization guide\](/apps-script/guides/services/authorization) for more details. |
| `@NotOnlyCurrentDoc` | Used in libraries to override an inherited `@OnlyCurrentDoc` annotation. |