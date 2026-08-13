# Filter

Modify existing filters on Grid sheets.

The Filter class is used to modify existing filters on Grid sheets (the default sheet type). Grid sheets are regular sheets with data that aren't connected to a database. To use this class, you must first access the grid sheet filter using `Range.getFilter()` or `Sheet.getFilter()`. If a filter doesn't exist yet, create one using `Range.createFilter()`.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `getColumnFilterCriteria(columnPosition: Integer)` | `FilterCriteria\|null` | Gets the filter criteria on the specified column, or `null` if the column doesn't have filter criteria applied. To get more details about the filter criteria, chain this method with methods from the FilterCriteria class. `columnPosition` is the 1-indexed position of the column. |
| `getRange()` | `Range` | Gets the range this filter applies to. To get the range in A1 notation, chain this method with `Range.getA1Notation()`. |
| `remove()` | `void` | Removes this filter. |
| `removeColumnFilterCriteria(columnPosition: Integer)` | `Filter` | Removes the filter criteria from the specified column. `columnPosition` is the 1-indexed position of the column. |
| `setColumnFilterCriteria(columnPosition: Integer, filterCriteria: FilterCriteria)` | `Filter` | Sets the filter criteria on the specified column. First, create the filter criteria builder using `SpreadsheetApp.newFilterCriteria()`. Then add criteria using the FilterCriteriaBuilder class. If you set the criteria to `null`, it removes filter criteria from the specified column. |
| `sort(columnPosition: Integer, ascending: Boolean)` | `Filter` | Sorts the filtered range by the specified column, excluding the first row (the header row) in the range this filter applies to. `columnPosition` is the 1-indexed position of the column; `ascending` — if `true`, sorts ascending; if `false`, sorts descending. |

## Code Samples

```javascript
const ss = SpreadsheetApp.getActiveSheet();
const filter = ss.getFilter();
const filterCriteria = filter.getColumnFilterCriteria(2).getHiddenValues();
console.log(filterCriteria);
```

```javascript
const ss = SpreadsheetApp.getActiveSheet();
const filter = ss.getFilter();
console.log(filter.getRange().getA1Notation());
```

```javascript
const ss = SpreadsheetApp.getActiveSheet();
const filter = ss.getFilter();
filter.remove();
```

```javascript
const ss = SpreadsheetApp.getActiveSheet();
const filter = ss.getFilter();
filter.removeColumnFilterCriteria(2);
```

```javascript
const ss = SpreadsheetApp.getActiveSheet();
const filter = ss.getFilter();
const criteria = SpreadsheetApp.newFilterCriteria()
                     .setHiddenValues(['Hello', 'World'])
                     .build();
filter.setColumnFilterCriteria(3, criteria);
```

```javascript
const ss = SpreadsheetApp.getActiveSheet();
const filter = ss.getFilter();
filter.sort(2, true);
```
