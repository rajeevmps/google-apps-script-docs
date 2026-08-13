# Banding

Access and modify bandings, the color patterns applied to rows or columns of a range.

Access and modify bandings, the color patterns applied to rows or columns of a range. Each banding consists of a range and a set of colors for rows, columns, headers, and footers. Banding refers to the color patterns applied to rows or columns of a range within a spreadsheet. Each banding is defined by a range and specific colors for its rows, columns, headers, and footers.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `copyTo(range: Range)` | `Banding` | Copies this banding to another range. |
| `getFirstColumnColorObject()` | `Color\|null` | Returns the first alternating column color in the banding, or `null` if no color is set. |
| `getFirstRowColorObject()` | `Color\|null` | Returns the first alternating row color, or `null` if no color is set. |
| `getFooterColumnColorObject()` | `Color\|null` | Returns the color of the last column in the banding, or `null` if no color is set. |
| `getFooterRowColorObject()` | `Color\|null` | Returns the last row color in the banding, or `null` if no color is set. |
| `getHeaderColumnColorObject()` | `Color\|null` | Returns the color of the first column in the banding, or `null` if no color is set. |
| `getHeaderRowColorObject()` | `Color\|null` | Returns the color of the header row or `null` if no color is set. |
| `getRange()` | `Range` | Returns the range for this banding. |
| `getSecondColumnColorObject()` | `Color\|null` | Returns the second alternating column color in the banding, or `null` if no color is set. |
| `getSecondRowColorObject()` | `Color\|null` | Returns the second alternating row color, or `null` if no color is set. |
| `remove()` | `void` | Removes this banding. |
| `setFirstColumnColor(color: String)` | `Banding` | Sets the first column color that is alternating. Color code in CSS notation or `null` to clear. |
| `setFirstColumnColorObject(color: Color)` | `Banding` | Sets the first alternating column color in the banding. |
| `setFirstRowColor(color: String)` | `Banding` | Sets the first row color that is alternating. |
| `setFirstRowColorObject(color: Color)` | `Banding` | Sets the first alternating row color in the banding. |
| `setFooterColumnColor(color: String)` | `Banding` | Sets the color of the last column. |
| `setFooterColumnColorObject(color: Color)` | `Banding` | Sets the color of the last column in the banding. |
| `setFooterRowColor(color: String)` | `Banding` | Sets the color of the last row. |
| `setFooterRowColorObject(color: Color)` | `Banding` | Sets the color of the footer row in the banding. |
| `setHeaderColumnColor(color: String)` | `Banding` | Sets the color of the header column. |
| `setHeaderColumnColorObject(color: Color)` | `Banding` | Sets the color of the header column. |
| `setHeaderRowColor(color: String)` | `Banding` | Sets the color of the header row. |
| `setHeaderRowColorObject(color: Color)` | `Banding` | Sets the color of the header row. |
| `setRange(range: Range)` | `Banding` | Sets the range for this banding. |
| `setSecondColumnColor(color: String)` | `Banding` | Sets the second column color that is alternating. |
| `setSecondColumnColorObject(color: Color)` | `Banding` | Sets the second alternating column color in the banding. |
| `setSecondRowColor(color: String)` | `Banding` | Sets the second row color that is alternating. |
| `setSecondRowColorObject(color: Color)` | `Banding` | Sets the second alternating color in the banding. |

### Deprecated Methods

| Method | Return Type | Description |
|---|---|---|
| `getFirstColumnColor()` | `String\|null` | Deprecated. Replaced by `getFirstColumnColorObject()`. |
| `getFirstRowColor()` | `String\|null` | Deprecated. Replaced by `getFirstRowColorObject()`. |
| `getFooterColumnColor()` | `String\|null` | Deprecated. Replaced by `getFooterColumnColorObject()`. |
| `getFooterRowColor()` | `String\|null` | Deprecated. Replaced by `getFooterRowColorObject()`. |
| `getHeaderColumnColor()` | `String\|null` | Deprecated. Replaced by `getHeaderColumnColorObject()`. |
| `getHeaderRowColor()` | `String\|null` | Deprecated. Replaced by `getHeaderRowColorObject()`. |
| `getSecondColumnColor()` | `String\|null` | Deprecated. Replaced by `getSecondColumnColorObject()`. |
| `getSecondRowColor()` | `String\|null` | Deprecated. Replaced by `getSecondRowColorObject()`. |

## Authorization

All methods require one or more of these scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`
