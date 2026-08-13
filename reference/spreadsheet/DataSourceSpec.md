# DataSourceSpec

Access the general settings of an existing data source spec.

Access the general settings of an existing data source spec. To access data source spec for certain type, use `as...()` method. To create a new data source spec, use `SpreadsheetApp.newDataSourceSpec()`. Only use this class with data that's connected to a database.

Key capabilities: use `as...()` methods to access data source specs for specific types like BigQuery or Looker; create a `DataSourceSpecBuilder` based on existing spec's settings using `copy()`; retrieve parameters and type of data source spec using `getParameters()` and `getType()`.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `asBigQuery()` | `BigQueryDataSourceSpec` | Gets the spec for BigQuery data source. |
| `asLooker()` | `LookerDataSourceSpec` | Gets the spec for Looker data source. |
| `copy()` | `DataSourceSpecBuilder` | Creates a `DataSourceSpecBuilder` based on this data source's settings. |
| `getParameters()` | `DataSourceParameter[]` | Gets the parameters of the data source. This method is only available for BigQuery data sources. |
| `getType()` | `DataSourceType` | Gets the type of the data source. |

## Code Samples

```javascript
const dataSourceTable = SpreadsheetApp.getActive()
    .getSheetByName('Data Sheet 1')
    .getDataSourceTables()[0];
const spec = dataSourceTable.getDataSource().getSpec();
if (spec.getType() === SpreadsheetApp.DataSourceType.BIGQUERY) {
  const bqSpec = spec.asBigQuery();
  Logger.log('Project ID: %s\n', bqSpec.getProjectId());
  Logger.log('Raw query string: %s\n', bqSpec.getRawQuery());
}
```

```javascript
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);
const spec = ss.getDataSources()[0].getSpec().asLooker();

if (spec.getType() === SpreadsheetApp.DataSourceType.LOOKER) {
  const lookerSpec = spec.asLooker();
  Logger.log('Looker instance URL: %s\n', lookerSpec.getInstanceUrl());
}
```

```javascript
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);
const spec = ss.getDataSources()[0].getSpec();
const parameters = spec.getParameters();
```

```javascript
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);
const spec = ss.getDataSources()[0].getSpec();
const type = spec.getType();
```
