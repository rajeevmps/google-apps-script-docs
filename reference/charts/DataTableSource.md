# DataTableSource

Interface for objects that can represent their data as a DataTable.

Interface for objects that can represent their data as a `DataTable`. Implementing classes include `DataTable` (a Data Table used in charts) and `Range` (provides access to modify spreadsheet ranges).

## Methods

### getDataTable()

Returns: `DataTable`

Return the data inside this object as a DataTable.

The method enables converting object data into a DataTable format suitable for chart creation. A typical example demonstrates retrieving a range from a spreadsheet and converting it to a DataTable, which can then be used with the Charts service to build visualizations.

## Properties

None.
