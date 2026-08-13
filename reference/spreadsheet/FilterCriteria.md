# FilterCriteria

Get information about or copy the criteria on existing filters.

Use this class to get information about or copy the criteria on existing filters. FilterCriteria enables retrieval and duplication of filter criteria information. Creation methods include `SpreadsheetApp.newFilterCriteria()` and `FilterCriteriaBuilder`. The class supports copying criteria between columns and retrieving color-based or value-based filter information.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `copy()` | `FilterCriteriaBuilder` | Copies this filter criteria and creates a criteria builder that you can apply to another filter. |
| `getCriteriaType()` | `BooleanCriteria\|null` | Returns the criteria's boolean type, for example, `CELL_EMPTY`. Returns null when criteria isn't a boolean condition. Commonly used alongside `getCriteriaValues()` for modifying existing criteria. |
| `getCriteriaValues()` | `Object[]` | Returns an array of arguments for boolean criteria. Some criteria types return empty arrays (e.g., `CELL_NOT_EMPTY`). Works with `FilterCriteriaBuilder.withCriteria()` for criteria modification. |
| `getHiddenValues()` | `String[]` | Returns the values that the filter hides. Use this criteria with filters on Grid sheets, the default type of sheet. Returns null for non-Grid filter types. |
| `getVisibleBackgroundColor()` | `Color\|null` | Returns the background color used as filter criteria. Cells with this background color remain visible. Applicable only to Grid sheets; returns null otherwise. |
| `getVisibleForegroundColor()` | `Color\|null` | Returns the foreground color used as a filter criteria. Cells with this foreground color remain visible. Grid sheet-specific; returns null for other filter types. |
| `getVisibleValues()` | `String[]` | Returns the values that the pivot table filter shows. This criteria is only for filters on pivot tables that aren't connected to a database. Returns empty array for non-pivot-table filters. |

## Code Samples

```javascript
const ss = SpreadsheetApp.getActiveSheet();
const range = ss.getRange('A1:C20');
const filter = range.getFilter();
const criteria = filter.getColumnFilterCriteria(3).copy().build();
filter.setColumnFilterCriteria(2, criteria);
```

```javascript
const ss = SpreadsheetApp.getActiveSheet();
const range = ss.getRange('A1:C20');
const filter = range.getFilter();
const filterCriteria = filter.getColumnFilterCriteria(2).getHiddenValues();
console.log(filterCriteria);
```

```javascript
const ss = SpreadsheetApp.getActiveSheet();
const filter = ss.getFilter();
const criteriaType = 
    filter.getColumnFilterCriteria(2).getCriteriaType().toString();
console.log(criteriaType);
```

```javascript
const ss = SpreadsheetApp.getActiveSheet();
const range = ss.getRange('A1:C20');
const filter = range.getFilter();
const color = filter.getColumnFilterCriteria(2)
                  .getVisibleBackgroundColor()
                  .asRgbColor()
                  .asHexString();
console.log(color);
```

```javascript
const ss = SpreadsheetApp.getActiveSheet();
const pivotTable = ss.getPivotTables()[0];
const pivotFilterValues = 
    pivotTable.getFilters()[0].getFilterCriteria().getVisibleValues();
console.log(pivotFilterValues);
```
