# DataSourceSpecBuilder

Builder for the general settings of a data source spec.

DataSourceSpecBuilder is used to create a specification for data sources connected to a database. To create a new builder, use `SpreadsheetApp.newDataSourceSpec()`. Specific database types like BigQuery and Looker have dedicated builder methods accessible via `asBigQuery()` and `asLooker()`. The `build()` method finalizes the specification from the builder's settings. Only use this class with data that's connected to a database.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `asBigQuery()` | `BigQueryDataSourceSpecBuilder` | Gets the builder for BigQuery data source. Returns the BigQuery data source specification builder. |
| `asLooker()` | `LookerDataSourceSpecBuilder` | Gets the builder for Looker data source. Returns the Looker data source specification builder. |
| `build()` | `DataSourceSpec` | Builds a data source specification from the settings in this builder. Must use `as...()` to specify a data source type before building. |
| `copy()` | `DataSourceSpecBuilder` | Creates a DataSourceSpecBuilder based on this data source's settings. Returns the builder. |
| `getParameters()` | `DataSourceParameter[]` | Gets the parameters of the data source. Available only for BigQuery data sources. Returns the parameter list. |
| `getType()` | `DataSourceType` | Gets the type of the data source. Returns the data source type. |
| `removeAllParameters()` | `DataSourceSpecBuilder` | Removes all the parameters. Returns the builder for chaining. |
| `removeParameter(parameterName: String)` | `DataSourceSpecBuilder` | Removes the specified parameter. `parameterName` is the name of the parameter to remove. Returns the builder for chaining. |
| `setParameterFromCell(parameterName: String, sourceCell: String)` | `DataSourceSpecBuilder` | Adds a parameter, or if the parameter with the name exists, updates its source cell for data source spec builders of type DataSourceType.BIGQUERY. Available only for BigQuery data sources. `parameterName` is the parameter name; `sourceCell` is the source cell in A1 notation. Returns the builder for chaining. |

## Code Samples

```javascript
const spec = SpreadsheetApp.newDataSourceSpec()
                 .asBigQuery()
                 .setProjectId('big_query_project')
                 .setRawQuery('select @FIELD from table limit @LIMIT')
                 .setParameterFromCell('FIELD', 'Sheet1!A1')
                 .setParameterFromCell('LIMIT', 'namedRangeCell')
                 .build();
```

```javascript
const spec = SpreadsheetApp.newDataSourceSpec()
                 .asLooker()
                 .setInstanceUrl('https://looker_instance_url.com')
                 .setModelName('model_name')
                 .setExploreName('explore_name')
                 .build();
```
