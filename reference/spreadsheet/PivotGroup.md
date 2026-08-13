# PivotGroup

Access and modify pivot table breakout groups.

Access and modify pivot table breakout groups.

## Methods

### `addManualGroupingRule(groupName, groupMembers)`

Adds a manual grouping rule for this pivot group.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| group Name | String | The name of this grouping rule. |
| group Members | Object[] | The values that are included in this grouping rule. |

**Returns:** PivotGroup — the pivot group for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `areLabelsRepeated()`

Returns whether labels are displayed as repeated.

**Returns:** Boolean — true if labels are repeated; otherwise returns false .

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `clearGroupingRule()`

Removes any grouping rules from this pivot group.

**Returns:** PivotGroup — the pivot group for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `clearSort()`

Removes any sorting applied to this group.

**Returns:** PivotGroup — the pivot group for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getDateTimeGroupingRule()`

Returns the date-time grouping rule on the pivot group, or null if no date-time
grouping rule is set.

**Returns:** DateTimeGroupingRule |null — The date-time grouping rule.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getDimension()`

Returns whether this is a row or column group.

**Returns:** Dimension — the dimension representing this group's type

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getGroupLimit()`

Returns the pivot group limit on the pivot group. Returns null if no pivot group limit
is set.

**Returns:** PivotGroupLimit |null — The pivot group limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getIndex()`

Returns the index of this pivot group in the current group order.

**Returns:** Integer — the pivot group's index

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getPivotTable()`

Returns the PivotTable which this grouping belongs to.

**Returns:** PivotTable — the pivot table this group belongs to.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getSourceDataColumn()`

Returns the number of the source data column this group summarizes. This index is 1-based, if
this group summarizes source data in column "A" of the spreadsheet this method returns 1 .

**Returns:** Integer — the source data column number

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getSourceDataSourceColumn()`

Returns the data source column the pivot group operates on. Returns null if the pivot
table is not a {DataSourcePivotTableApi}.

**Returns:** DataSourceColumn |null — The data source column the pivot group operates on.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `hideRepeatedLabels()`

Hides repeated labels for this grouping. If labels are already hidden this results in a no-op.
If this method is called before there are multiple row or column groupings, when an additional
grouping is added repeated labels are hidden.

**Returns:** PivotGroup — the pivot group for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `isSortAscending()`

Returns true if the sort is ascending, returns false if the sort order is
descending.

**Returns:** Boolean — true if the sort order is ascending.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `moveToIndex(index)`

Moves this group to the specified position in the current list of row or column groups. These
indices are 0-based. For example, if this group should be moved to the first position this
method should be called with 0 .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| index | Integer | The index to move this grouping to. |

**Returns:** PivotGroup — the pivot group for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `remove()`

Removes this pivot group from the table.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `removeManualGroupingRule(groupName)`

Removes the manual grouping rule with the specified groupName .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| group Name | String | The name of the grouping rule to remove. |

**Returns:** PivotGroup — the pivot group for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `resetDisplayName()`

Resets the display name of this group in the pivot table to its default value.

**Returns:** PivotGroup — the pivot group for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setDateTimeGroupingRule(dateTimeGroupingRuleType)`

Sets the date-time grouping rule on the pivot group.

To remove the rule, use clearGroupingRule() .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| date Time Grouping Rule Type | Date Time Grouping Rule Type | The rule type to set. |

**Returns:** PivotGroup — The pivot group, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setDisplayName(name)`

Sets the display name of this group in the pivot table.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| name | String | The display name to set. |

**Returns:** PivotGroup — the pivot group for chaining

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setGroupLimit(countLimit)`

Sets the pivot group limit on the pivot group. The operation is only supported for DataSourcePivotTable .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| count Limit | Integer | The count limit of rows or columns to set. Must be positive. |

**Returns:** PivotGroup — The pivot group for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setHistogramGroupingRule(minValue, maxValue, intervalSize)`

Sets a histogram grouping rule for this pivot group. A histogram rule organizes values in a
source data column into buckets of a constant size. All values from minValue to maxValue are placed into groups of size interval . All values below minValue are placed into one bucket, as are all values greater than maxValue .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| min Value | Integer | The minimum value for items to be placed into buckets. Values less than this
    are combined into a single bucket. |
| max Value | Integer | The maximum value for items to be placed into buckets. Values greater than this
    are combined into a single bucket. |
| interval Size | Integer |  |

**Returns:** PivotGroup — the pivot group for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `showRepeatedLabels()`

When there is more than one row or column grouping, this method displays this grouping's label
for each entry of the subsequent grouping. If labels are already repeated this results in a
no-op. If this method is called before there are multiple row or column groupings, when an
additional grouping is added repeated labels are shown.

**Returns:** PivotGroup — the pivot group for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `showTotals(showTotals)`

Sets whether to show total values for this pivot group in the table.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| show Totals | Boolean | Whether to show totals or not. |

**Returns:** PivotGroup — the pivot group for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `sortAscending()`

Sets the sort order to be ascending.

**Returns:** PivotGroup — the pivot group for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `sortBy(value, oppositeGroupValues)`

Sorts this group by the specified PivotValue for the values from the oppositeGroupValues .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| value | Pivot Value | The pivot value to sort by. |
| opposite Group Values | Object[] | The values of an opposite pivot group (a column group if sorting a
    row group, or a row group if sorting a column group) that are used to sort. The order of
    these values determines precedence for tie breaking. |

**Returns:** PivotGroup — the pivot group for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Sorts the item group by the "SUM of Quantity" pivot value for the specified
// salespersons.
const sheet = SpreadsheetApp.getActiveSheet();
const pivotTable = sheet.getPivotTables()[0];
const itemGroup = pivotTable.getRowGroups()[0];
const sumQuantityValue = pivotTable.getPivotValues()[0];
itemGroup.sortBy(sumQuantityValue, ['Beth', 'Amir', 'Devyn']);
```

### `sortDescending()`

Sets the sort order to be descending.

**Returns:** PivotGroup — the pivot group for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `totalsAreShown()`

Returns whether total values are currently shown for this pivot group.

**Returns:** Boolean — true if total values are displayed for this pivot group; otherwise returns false .

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

