# DataViewDefinitionBuilder

Builder for DataViewDefinition objects.

Builder for `DataViewDefinition` objects. This class is used to construct `DataViewDefinition` instances that define which columns from a data source should be included in a data view, with optional role specifications for those columns.

## Methods

### build()

Returns: `DataViewDefinition`

Builds and returns the data view definition object that was built using this builder.

### setColumns(columns)

Returns: `DataViewDefinitionBuilder`

Sets the indexes of the columns to include in the data view as well as specifying role-column information. The method accepts an array of column indexes or column description objects. Column descriptions can define roles describing the purpose of data in that column (such as tooltip text, annotations, or uncertainty indicators). The column indexes are zero-based and reference columns from the underlying data source. The method enables role-based styling where columns can be designated for purposes like visual styling of chart elements based on their data values.

**Parameters**

| Name | Type | Description |
|---|---|---|
| columns | Object[] | the indexes of the columns to include, or column description objects specifying role information |

## Properties

None.
