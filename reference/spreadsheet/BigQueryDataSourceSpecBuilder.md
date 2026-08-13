# BigQueryDataSourceSpecBuilder

Builder for a BigQuery data source specification.

BigQueryDataSourceSpecBuilder is the builder for constructing BigQuery data source specifications. It provides methods to configure dataset ID, project ID, table ID, raw query strings, and parameters for BigQuery-connected data sources in Google Sheets.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `build()` | `DataSourceSpec` | Builds a data source specification from the settings in this builder. Must use `as...()` to specify a data source type before building. |
| `copy()` | `DataSourceSpecBuilder` | Creates a `DataSourceSpecBuilder` based on this data source's settings. |
| `getDatasetId()` | `String` | Gets the BigQuery dataset ID. Returns empty string if spec defined by raw query. |
| `getParameters()` | `DataSourceParameter[]` | Gets the parameters of the data source. Available only for BigQuery sources. |
| `getProjectId()` | `String` | Gets the billing project ID. |
| `getRawQuery()` | `String` | Gets the raw query string. |
| `getTableId()` | `String` | Gets the BigQuery table ID. Returns empty string if spec defined by raw query. |
| `getTableProjectId()` | `String` | Gets the BigQuery project ID for the table. Returns empty string if spec defined by raw query. |
| `getType()` | `DataSourceType` | Gets the type of the data source. |
| `removeAllParameters()` | `BigQueryDataSourceSpecBuilder` | Removes all the parameters. Returns builder for chaining. |
| `removeParameter(parameterName: String)` | `BigQueryDataSourceSpecBuilder` | Removes the specified parameter. Returns builder for chaining. |
| `setDatasetId(datasetId: String)` | `BigQueryDataSourceSpecBuilder` | Sets the BigQuery dataset ID. Returns builder for chaining. |
| `setParameterFromCell(parameterName: String, sourceCell: String)` | `BigQueryDataSourceSpecBuilder` | Adds a parameter, or if the parameter with the name exists, updates its source cell for data source spec builders of type `DataSourceType.BIGQUERY`. Available for BigQuery only. |
| `setProjectId(projectId: String)` | `BigQueryDataSourceSpecBuilder` | Sets the billing BigQuery project ID. Returns builder for chaining. |
| `setRawQuery(rawQuery: String)` | `BigQueryDataSourceSpecBuilder` | Sets the raw query string. Returns builder for chaining. |
| `setTableId(tableId: String)` | `BigQueryDataSourceSpecBuilder` | Sets the BigQuery table ID. Returns builder for chaining. |
| `setTableProjectId(projectId: String)` | `BigQueryDataSourceSpecBuilder` | Sets the BigQuery project ID for the table. Returns builder for chaining. |

## Code Samples

```javascript
const bigQueryDataSourceSpec = SpreadsheetApp.newDataSourceSpec().asBigQuery();
bigQueryDataSourceSpec.setDatasetId('my data set id');
bigQueryDataSourceSpec.setProjectId('my project id');
bigQueryDataSourceSpec.setTableId('my table id');
bigQueryDataSourceSpec.build();
```

```javascript
const specBuilder = SpreadsheetApp.newDataSourceSpec().asBigQuery();
specBuilder.setParameterFromCell('x', 'A1');
const bigQuerySpec = specBuilder.build();
```

```javascript
const ss = SpreadsheetApp.openByUrl('https://docs.google.com/spreadsheets/d/abc123456/edit');
const spec = ss.getDataSources()[0].getSpec();
const parameters = spec.getParameters();
```
