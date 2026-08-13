# TextFinder

Find or replace text within a range, sheet or spreadsheet.

Find or replace text within a range, sheet or spreadsheet. Can also specify search options.

## Methods

### `findAll()`

Returns all cells matching the search criteria.

**Returns:** Range[] — All the matching cells.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `findNext()`

Returns the next cell matching the search criteria.

**Returns:** Range — The next matching cell, or null if there are no previous matches.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `findPrevious()`

Returns the previous cell matching the search criteria.

**Returns:** Range — The previous matching cell, or null if there are no previous matches.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getCurrentMatch()`

Returns the current cell matching the search criteria.

**Returns:** Range — The current matching cell, or null if there are no further matches.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `ignoreDiacritics(ignoreDiacritics)`

If true , configures the search to ignore diacritics while matching; otherwise the
search matches diacritics. A diacritic is a sign, such as an accent or cedilla, which when
written above or below a letter indicates a difference in pronunciation from the same letter
when unmarked or differently marked.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| ignore Diacritics | Boolean | Whether the search considers diacritics. |

**Returns:** TextFinder — This text finder, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `matchCase(matchCase)`

If true , configures the search to match the search text's case exactly, otherwise the
search defaults to case-insensitive matching.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| match Case | Boolean | Whether the matching is case-sensitive. |

**Returns:** TextFinder — This text finder, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `matchEntireCell(matchEntireCell)`

If true , configures the search to match the entire contents of a cell; otherwise, the
search defaults to partial matching.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| match Entire Cell | Boolean | Whether the entire cell is matched. |

**Returns:** TextFinder — This text finder, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `matchFormulaText(matchFormulaText)`

If true , configures the search to return matches that appear within formula text;
otherwise cells with formulas are considered based on their displayed value.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| match Formula Text | Boolean | Whether the search examines formula text. |

**Returns:** TextFinder — This text finder, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `replaceAllWith(replaceText)`

Replaces all matches with the specified text. Returns the number of occurrences replaced, which
may be different from the number of matched cells.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| replace Text | String | The text that replaces the text in the matched cells. |

**Returns:** Integer — The number of occurrences replaced.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `replaceWith(replaceText)`

Replaces the search text in the currently matched cell with the specified text and returns the
number of occurrences replaced.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| replace Text | String | The text that replaces the content in the currently matched cell. |

**Returns:** Integer — The number of occurrences replaced.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `startFrom(startRange)`

Configures the search to start searching immediately after the specified cell range.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| start Range | Range | The cell range after which the search should start. |

**Returns:** TextFinder — This text finder, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `useRegularExpression(useRegEx)`

If true , configures the search to interpret the search string as a regular expression;
otherwise the search interprets the search string as normal text. For more details on how to
use regular expressions, refer to the Find and replace support page.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| use Reg Ex | Boolean | Whether to interpret the search string as a regular expression. |

**Returns:** TextFinder — This text finder, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

