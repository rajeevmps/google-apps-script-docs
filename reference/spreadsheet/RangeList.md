# RangeList

A collection of one or more Range instances in the same sheet.

A collection of one or more Range instances in the same sheet. You can use this class
to apply operations on collections of non-adjacent ranges or cells.

## Methods

### `activate()`

Selects the list of Range instances. The last range in the list is set as the active range .

Note: This provides a way to multi-select a number of ranges.

**Returns:** RangeList — The list of active ranges, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['D4', 'B2:C4']);
rangeList.activate();

const selection = sheet.getSelection();
// Current cell: B2
const currentCell = selection.getCurrentCell();
// Active range: B2:C4
const activeRange = selection.getActiveRange();
// Active range list: [D4, B2:C4]
const activeRangeList = selection.getActiveRangeList();
```

### `breakApart()`

Break all horizontally- or vertically-merged cells contained within the range list into
individual cells again.

Calling this function on a range list is equivalent to selecting a set of ranges and
selecting the Format > Merge > Unmerge Sheets menu item.

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
rangeList.breakApart();
```

### `check()`

Changes the state of the checkboxes in the range to “checked”. Ignores the cells in the range
which currently do not contain either the checked or unchecked value configured.

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Changes the state of cells which currently contain either the checked or
// unchecked value configured in the ranges D4 and E6 to 'checked'.
const rangeList = SpreadsheetApp.getActive().getRangeList(['D4', 'E6']);
rangeList.check();
```

### `clear()`

Clears the range of contents, formats, and data validation rules for each Range in
the range list.

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
rangeList.clear();
```

### `clear(options)`

Clears the range of contents, format, data validation rules, and comments, as specified with
the given options. By default all data is cleared.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| options | Object | A JavaScript object that specifies advanced parameters, as listed below. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// The code below clears the contents of the following ranges A:A and C:C in the
// active sheet, but preserves the format, data validation rules, and comments.
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
rangeList.clear({contentsOnly: true});
```

### `clearContent()`

Clears the content of each Range in the range list, leaving the formatting intact.

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
rangeList.clearContent();
```

### `clearDataValidations()`

Clears the data validation rules for each Range in the range list.

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
rangeList.clearDataValidations();
```

### `clearFormat()`

Clears text formatting for each Range in the range list.

This clears text formatting for each range, but does not reset any number formatting rules.

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
rangeList.clearFormat();
```

### `clearNote()`

Clears the note for each Range in the range list.

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
rangeList.clearNote();
```

### `getRanges()`

Returns a list of one or more Range instances in the same sheet.

**Returns:** Range[] — The list of ranges.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `insertCheckboxes()`

Inserts checkboxes into each cell in the range, configured with true for checked and false for unchecked. Sets the value of all cells in the range to false .

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const rangeList = SpreadsheetApp.getActive().getRangeList(['D4', 'E6']);

// Inserts checkboxes into each cell in the ranges D4 and E6 configured with
// 'true' for checked and 'false' for unchecked. Also, sets the value of each
// cell in the ranges D4 and E6 to 'false'.
rangeList.insertCheckboxes();
```

### `insertCheckboxes(checkedValue)`

Inserts checkboxes into each cell in the range, configured with a custom value for checked and
the empty string for unchecked. Sets the value of each cell in the range to the empty string.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| checked Value | Object | The checked value for the checkbox data validation. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const rangeList = SpreadsheetApp.getActive().getRangeList(['D4', 'E6']);

// Inserts checkboxes into each cell in the ranges D4 and E6 configured with
// 'yes' for checked and the empty string for unchecked. Also, sets the value of
// each cell in the ranges D4 and E6 to the empty string.
rangeList.insertCheckboxes('yes');
```

### `insertCheckboxes(checkedValue, uncheckedValue)`

Inserts checkboxes into each cell in the range, configured with custom values for the checked
and unchecked states. Sets the value of each cell in the range to the custom unchecked value.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| checked Value | Object | The checked value for the checkbox data validation. |
| unchecked Value | Object | The unchecked value for the checkbox data validation. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const rangeList = SpreadsheetApp.getActive().getRangeList(['D4', 'E6']);

// Inserts checkboxes into each cell in the ranges D4 and E6 configured with
// 'yes' for checked and 'no' for unchecked. Also, sets the value of each cell
// in the ranges D4 and E6 to 'no'.
rangeList.insertCheckboxes('yes', 'no');
```

### `removeCheckboxes()`

Removes all checkboxes from the range. Clears the data validation of each cell, and
additionally clears its value if the cell contains either the checked or unchecked value.

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const range = SpreadsheetApp.getActive().getRange('A1:B10');

// Inserts checkboxes and sets each cell value to 'no' in the range A1:B10.
range.insertCheckboxes('yes', 'no');

const rangeList1 = SpreadsheetApp.getActive().getRangeList(['A1', 'A3']);
rangeList1.setValue('yes');
// Removes the checkbox data validation in cells A1 and A3 and clears their
// value.
rangeList1.removeCheckboxes();

const rangeList2 = SpreadsheetApp.getActive().getRangeList(['A5', 'A7']);
rangeList2.setValue('random');
// Removes the checkbox data validation in cells A5 and A7 but does not clear
// their value.
rangeList2.removeCheckboxes();
```

### `setBackground(color)`

Sets the background color for each Range in the range list. Color is represented in
in CSS notation; for example, '#ffffff' or 'white' .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| color | String | The background color code in CSS notation such as '#ffffff' or 'white' ; a null value resets the color. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
rangeList.setBackground('red');
```

### `setBackgroundRGB(red, green, blue)`

Sets the background to the given RGB color. This is a convenience wrapper around a setBackground(color) call.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| red | Integer | The red value in RGB notation. |
| green | Integer | The green value in RGB notation. |
| blue | Integer | The blue value in RGB notation. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
// Sets the background to red for each range in the range list.
rangeList.setBackgroundRGB(255, 0, 0);
```

### `setBorder(top, left, bottom, right, vertical, horizontal)`

Sets the border property for each Range in the range list. The valid values are true (on), false (off) and null (no change).

**Parameters:**

| Name | Type | Description |
|---|---|---|
| top | Boolean | true for border, false for none, null for no change. |
| left | Boolean | true for border, false for none, null for no change. |
| bottom | Boolean | true for border, false for none, null for no change. |
| right | Boolean | true for border, false for none, null for no change. |
| vertical | Boolean | true for internal vertical borders, false for none, null for no change. |
| horizontal | Boolean | true for internal horizontal borders, false for none, null for no change. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A2:B4', 'C1:D4']);
// Sets borders on the top and bottom of the ranges A2:B4 and C1:D4, but leaves
// the left and right unchanged.
rangeList.setBorder(true, null, true, null, false, false);
```

### `setBorder(top, left, bottom, right, vertical, horizontal, color, style)`

Sets the border property with color and/or style for each Range in the range list.
Valid values are true (on), false (off) and null (no change). Color is
represented in CSS notation; for example, '#ffffff' or 'white' .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| top | Boolean | true for border, false for none, null for no change. |
| left | Boolean | true for border, false for none, null for no change. |
| bottom | Boolean | true for border, false for none, null for no change. |
| right | Boolean | true for border, false for none, null for no change. |
| vertical | Boolean | true for internal vertical borders, false for none, null for no change. |
| horizontal | Boolean | true for internal horizontal borders, false for none, null for no change. |
| color | String | The border color in CSS notation like '#ffffff' or 'white' , null for default color (black). |
| style | Border Style | The style for the borders, null for default style (solid). |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A2:B4', 'C1:D4']);
// Sets borders on the top and bottom, but leaves the left and right unchanged
// of the ranges A2:B4 and C1:D4. Also sets the color to 'red', and the border
// to 'DASHED'.
rangeList.setBorder(
    true,
    null,
    true,
    null,
    false,
    false,
    'red',
    SpreadsheetApp.BorderStyle.DASHED,
);
```

### `setFontColor(color)`

Sets the font color for each Range in the range list. Color is represented in CSS
notation; for example, '#ffffff' or 'white' .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| color | String | The font color in CSS notation such as '#ffffff' or 'white' ; a null value resets the color. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
rangeList.setFontColor('red');
```

### `setFontFamily(fontFamily)`

Sets the font family for each Range in the range list. The font family is described
by a string identifier such as Arial or Roboto .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| font Family | String | The font family to set; a null value resets the font family. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
rangeList.setFontFamily('Roboto');
```

### `setFontLine(fontLine)`

Sets the font line style for each Range in the range list. The line styles options
are 'underline' , 'line-through' , or 'none' .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| font Line | String | The font line style, either 'underline' , 'line-through' , or 'none' ; a null value resets the font line style. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
rangeList.setFontLine('line-through');
```

### `setFontSize(size)`

Sets the font size (in points) for each Range in the range list.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| size | Integer | A font point size. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
rangeList.setFontSize(20);
```

### `setFontStyle(fontStyle)`

Set the font style for each Range in the range list. The font style options are 'italic' or 'normal' .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| font Style | String | The font style, either 'italic' or 'normal' ; a null value resets the font style. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
rangeList.setFontStyle('italic');
```

### `setFontWeight(fontWeight)`

Set the font weight for each Range in the range list. The font weight options are 'normal' or 'bold' .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| font Weight | String | The font weight, either 'bold' or 'normal' ; a null value resets the font weight. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
rangeList.setFontWeight('bold');
```

### `setFormula(formula)`

Updates the formula for each Range in the range list. The given formula must be in
A1 notation.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| formula | String | A string representing the formula to set. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A11', 'C11']);
rangeList.setFormula('=SUM(B1:B10)');
```

### `setFormulaR1C1(formula)`

Updates the formula for each Range in the range list. The given formula must be in
R1C1 notation.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| formula | String | A string formula. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A11', 'C11']);
// This sets the formula to be the sum of the 3 rows above B5
rangeList.setFormulaR1C1('=SUM(R[-3]C[0]:R[-1]C[0])');
```

### `setHorizontalAlignment(alignment)`

Set the horizontal alignment for each Range in the range list. The alignment options
are 'left' , 'center' , or 'right' .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| alignment | String | The alignment, either 'left' , 'center' or 'normal' ; a null value resets the alignment. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
rangeList.setHorizontalAlignment('center');
```

### `setNote(note)`

Sets the note text for each Range in the range list.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| note | String | The note text to set; a null value removes the note. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
rangeList.setNote('This is a note');
```

### `setNumberFormat(numberFormat)`

Sets the number or date format for each Range in the range list.

The accepted formatting patterns are described in the Sheets API date and number formatting guide .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| number Format | String | A number format string. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A1:A10', 'C1:C10']);
// Always show 3 decimal points for the specified ranges.
rangeList.setNumberFormat('0.000');
```

### `setShowHyperlink(showHyperlink)`

Sets whether or not each Range in the range list should show hyperlinks.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| show Hyperlink | Boolean | Whether or not to show the hyperlink. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A1:A10', 'C1:C10']);
// Show hyperlinks for all the ranges.
rangeList.setShowHyperlink(true);
```

### `setTextDirection(direction)`

Sets the text direction for the cells in each Range in the range list. If a
specified direction is null , the direction is inferred and then set.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| direction | Text Direction | The desired text direction; if null the direction is inferred before
    setting. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Sets right-to-left text direction each range in the range list.
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A1:A10', 'C1:C10']);
rangeList.setTextDirection(SpreadsheetApp.TextDirection.RIGHT_TO_LEFT);
```

### `setTextRotation(degrees)`

Sets the text rotation settings for the cells in each Range in the range list. The
input corresponds to the angle between the standard text orientation and the desired
orientation. An input of zero indicates that the text is set to the standard orientation.

For left to right text direction, positive angles are in the counterclockwise direction,
whereas for right to left they are in the clockwise direction.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| degrees | Integer | The desired angle between the standard orientation and the desired orientation.
    For left to right text, positive angles are in the counterclockwise direction. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Sets the cells in the ranges A1:A10 and C1:C10 to have text rotated up 45
// degrees.
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['A1:A10', 'C1:C10']);
rangeList.setTextRotation(45);
```

### `setValue(value)`

Sets the value for each Range in the range list. The value can be numeric, string,
boolean or date. If it begins with '=' it is interpreted as a formula.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| value | Object | The value for the range. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
// Set value of 100 to each range in the range list.
const rangeList = sheet.getRangeList(['A:A', 'C:C']);
rangeList.setValue(100);
```

### `setVerticalAlignment(alignment)`

Set the vertical alignment for each Range in the range list. The alignment options
are 'top' , 'middle' or 'bottom' .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| alignment | String | The alignment, either 'top' , 'middle' or 'bottom' ; a null value resets the alignment. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Sets the vertical alignment to middle for the list of ranges.
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['D4', 'B2:C4']);
rangeList.setVerticalAlignment('middle');
```

### `setVerticalText(isVertical)`

Sets whether or not to stack the text for the cells for each Range in the range
list. If the text is stacked vertically, the degree text rotation setting is ignored.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| is Vertical | Boolean | Whether or not to stack the text. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Sets all cell's in ranges D4 and B2:D4 to have vertically stacked text.
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['D4', 'B2:C4']);
rangeList.setVerticalText(true);
```

### `setWrap(isWrapEnabled)`

Set text wrapping for each Range in the range list. Cells with wrap enabled resize
to display their full content. Cells with wrap disabled display as much as possible in the cell
without resizing or running to multiple lines.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| is Wrap Enabled | Boolean | Whether to wrap text or not. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Enable text wrap for the list of ranges.
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['D4', 'B2:C4']);
rangeList.setWrap(true);
```

### `setWrapStrategy(strategy)`

Sets the text wrapping strategy for each Range in the range list.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| strategy | Wrap Strategy | The desired wrapping strategy. |

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Sets the list of ranges to use the clip wrap strategy.
const sheet = SpreadsheetApp.getActiveSheet();
const rangeList = sheet.getRangeList(['D4', 'B2:C4']);
rangeList.setWrapStrategy(SpreadsheetApp.WrapStrategy.CLIP);
```

### `trimWhitespace()`

Trims the whitespace (such as spaces, tabs, or new lines) in every cell in this range list.
Removes all whitespace from the start and end of each cell's text, and reduces any subsequence
of remaining whitespace characters to a single space.

Note : If the resulting trimmed text starts with a '+' or '='
character, the text remains as a string value and isn't interpreted as a formula.

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheets()[0];
const range = sheet.getRange('A1:A4');
range.activate();
range.setValues([
  ' preceding space',
  'following space ',
  'two  middle  spaces',
  '   =SUM(1,2)',
]);

const rangeList = sheet.getRangeList(['A1', 'A2', 'A3', 'A4']);
rangeList.trimWhitespace();

const values = range.getValues();
// Values are ['preceding space', 'following space', 'two middle spaces',
// '=SUM(1,2)']
```

### `uncheck()`

Changes the state of the checkboxes in the range to “unchecked”. Ignores the cells in the range
which currently do not contain either the checked or unchecked value configured.

**Returns:** RangeList — This range list, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Changes the state of cells which currently contain either the checked or
// unchecked value configured in the ranges D4 and E6 to 'unchecked'.
const rangeList = SpreadsheetApp.getActive().getRangeList(['D4', 'E6']);
rangeList.uncheck();
```

