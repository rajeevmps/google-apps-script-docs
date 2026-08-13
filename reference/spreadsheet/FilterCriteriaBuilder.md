# FilterCriteriaBuilder

Builder for filter criteria.

Builder for filter criteria. To add criteria to a filter, you must do the following: 1. Create the criteria builder using `SpreadsheetApp.newFilterCriteria()`. 2. Add settings to the builder using the methods from this class. 3. Use `build()` to assemble the criteria with your specified settings.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `build()` | `FilterCriteria` | Assembles the filter criteria using the settings you add to the criteria builder. |
| `copy()` | `FilterCriteriaBuilder` | Copies this filter criteria and creates a criteria builder that you can apply to another filter. |
| `getCriteriaType()` | `BooleanCriteria\|null` | Returns the criteria's boolean type, for example, `CELL_EMPTY`. To learn about the types of boolean criteria, see the `BooleanCriteria` enum. |
| `getCriteriaValues()` | `Object[]` | Returns an array of arguments for boolean criteria. Some boolean criteria types don't have arguments and return an empty array, for example, `CELL_NOT_EMPTY`. |
| `getHiddenValues()` | `String[]` | Returns the values that the filter hides. Use this criteria with filters on Grid sheets, the default type of sheet. Returns `null` if you call this method for other types of filters. |
| `getVisibleBackgroundColor()` | `Color\|null` | Returns the background color used as filter criteria. Cells with this background color remain visible. Use this criteria with filters on Grid sheets, the default type of sheet. |
| `getVisibleForegroundColor()` | `Color\|null` | Returns the foreground color used as a filter criteria. Cells with this foreground color remain visible. Use this criteria with filters on Grid sheets, the default type of sheet. |
| `getVisibleValues()` | `String[]` | Returns the values that the pivot table filter shows. This criteria is only for filters on pivot tables that aren't connected to a database. |
| `setHiddenValues(values: String[])` | `FilterCriteriaBuilder` | Sets the values to hide. Clears any existing visible or hidden values. You can only use this criteria for filters on Grid sheets, the default type of sheet. Throws Error if any of the values are `null`. |
| `setVisibleBackgroundColor(visibleBackgroundColor: Color)` | `FilterCriteriaBuilder` | Sets the background color used as filter criteria. Cells with this background color remain visible. Setting a background color filter criteria removes any current color filter criteria from this builder. |
| `setVisibleForegroundColor(visibleForegroundColor: Color)` | `FilterCriteriaBuilder` | Sets the foreground color used as filter criteria. Cells with this foreground color remain visible. Setting a foreground color filter criteria removes any current color filter criteria from this builder. |
| `setVisibleValues(values: String[])` | `FilterCriteriaBuilder` | Sets the values to show on a pivot table. Clears any existing visible or hidden values. You can only use this criteria for filters on pivot tables that aren't connected to a database. Throws Error if any of the values are `null`. |
| `whenCellEmpty()` | `FilterCriteriaBuilder` | Sets the filter criteria to show empty cells. You can use this criteria with any type of filter. |
| `whenCellNotEmpty()` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells that aren't empty. You can use this criteria with any type of filter. |
| `whenDateAfter(date: Date)` | `FilterCriteriaBuilder` | Sets filter criteria that shows cells with dates that are after the specified date. You can use this criteria with any type of filter. |
| `whenDateAfter(date: RelativeDate)` | `FilterCriteriaBuilder` | Sets filter criteria that shows cells with dates that are after the specified relative date. |
| `whenDateBefore(date: Date)` | `FilterCriteriaBuilder` | Sets filter criteria that shows cells with dates that are before the specified date. You can use this criteria with any type of filter. |
| `whenDateBefore(date: RelativeDate)` | `FilterCriteriaBuilder` | Sets filter criteria that shows cells with dates that are before the specified relative date. |
| `whenDateEqualTo(date: Date)` | `FilterCriteriaBuilder` | Sets filter criteria that shows cells with dates that are equal to the specified date. You can use this criteria with any type of filter. |
| `whenDateEqualTo(date: RelativeDate)` | `FilterCriteriaBuilder` | Sets filter criteria that shows cells with dates that are equal to the specified relative date. |
| `whenDateEqualToAny(dates: Date[])` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with dates that are equal to any of the specified dates. |
| `whenDateNotEqualTo(date: Date)` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells that aren't equal to the specified date. |
| `whenDateNotEqualToAny(dates: Date[])` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with dates that aren't equal to any of the specified dates. |
| `whenFormulaSatisfied(formula: String)` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with a specified formula (such as `=B:B<C:C`) that evaluates to `true`. |
| `whenNumberBetween(start: Number, end: Number)` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with a number that falls between, or is either of, 2 specified numbers. |
| `whenNumberEqualTo(number: Number)` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with a number that's equal to the specified number. |
| `whenNumberEqualToAny(numbers: Number[])` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with a number that's equal to any of the specified numbers. |
| `whenNumberGreaterThan(number: Number)` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with a number greater than the specified number. |
| `whenNumberGreaterThanOrEqualTo(number: Number)` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with a number greater than or equal to the specified number. |
| `whenNumberLessThan(number: Number)` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with a number that's less than the specified number. |
| `whenNumberLessThanOrEqualTo(number: Number)` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with a number less than or equal to the specified number. |
| `whenNumberNotBetween(start: Number, end: Number)` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with a number doesn't fall between, and is neither of, 2 specified numbers. |
| `whenNumberNotEqualTo(number: Number)` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with a number that isn't equal to the specified number. |
| `whenNumberNotEqualToAny(numbers: Number[])` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with a number that isn't equal to any of the specified numbers. |
| `whenTextContains(text: String)` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with text that contains the specified text. |
| `whenTextDoesNotContain(text: String)` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with text that doesn't contain the specified text. |
| `whenTextEndsWith(text: String)` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with text that ends with the specified text. |
| `whenTextEqualTo(text: String)` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with text that's equal to the specified text. |
| `whenTextEqualToAny(texts: String[])` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with text that's equal to any of the specified text values. |
| `whenTextNotEqualTo(text: String)` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with text that isn't equal to the specified text. |
| `whenTextNotEqualToAny(texts: String[])` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with text that isn't equal to any of the specified values. |
| `whenTextStartsWith(text: String)` | `FilterCriteriaBuilder` | Sets the filter criteria to show cells with text that starts with the specified text. |
| `withCriteria(criteria: BooleanCriteria, args: Object[])` | `FilterCriteriaBuilder` | Sets the filter criteria to a boolean condition defined by `BooleanCriteria` values, such as `CELL_EMPTY` or `NUMBER_GREATER_THAN`. |

## Code Samples

```javascript
const ss = SpreadsheetApp.getActiveSheet();
const filter = ss.getFilter();
const criteria = SpreadsheetApp.newFilterCriteria()
                     .setHiddenValues(['hello', 'world'])
                     .build();
filter.setColumnFilterCriteria(3, criteria);
```

```javascript
const sheet = SpreadsheetApp.getActiveSpreadsheet()
                  .getSheetByName('Connected sheet')
                  .asDataSourceSheet();
const criteria = SpreadsheetApp.newFilterCriteria().whenCellNotEmpty().build();
sheet.addFilter('Category', criteria);
```

```javascript
const ss = SpreadsheetApp.getActiveSheet();
const filter = ss.getFilter();
const criteria = SpreadsheetApp
                     .newFilterCriteria()
                     .whenCellNotEmpty()
                     .build();
filter.setColumnFilterCriteria(2, criteria);
```

```javascript
const ss = SpreadsheetApp.getActiveSheet();
const filter = ss.getFilter();
const criteria = filter.getColumnFilterCriteria(3).copy().build();
filter.setColumnFilterCriteria(2, criteria);
```
