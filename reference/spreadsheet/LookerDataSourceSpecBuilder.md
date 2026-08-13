# LookerDataSourceSpecBuilder

Builder for a Looker data source specification.

The `LookerDataSourceSpecBuilder` is a builder class used to create and configure Looker Data Source specifications within Google Apps Script. It allows developers to construct data source specifications by configuring Looker-specific settings, then build the final specification using the `build()` method.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `build()` | `DataSourceSpec` | Builds a data source specification from the settings in this builder. Must use `as...()` to specify a data source type before building. |
| `copy()` | `DataSourceSpecBuilder` | Creates a `DataSourceSpecBuilder` based on this data source's settings. |
| `getExploreName()` | `String` | Gets the name of the Looker explore in the model. |
| `getInstanceUrl()` | `String` | Gets the URL of the Looker instance. |
| `getModelName()` | `String` | Gets the name of the Looker model in the instance. |
| `getParameters()` | `DataSourceParameter[]` | Gets the parameters of the data source. This method is only available for BigQuery data sources. |
| `getType()` | `DataSourceType` | Gets the type of the data source. |
| `removeAllParameters()` | `LookerDataSourceSpecBuilder` | Removes all the parameters. |
| `removeParameter(parameterName: String)` | `LookerDataSourceSpecBuilder` | Removes the specified parameter. `parameterName` is the name of the parameter to remove. |
| `setExploreName(exploreName: String)` | `LookerDataSourceSpecBuilder` | Sets the explore name in the Looker model. `exploreName` is the explore name in the selected Looker model. |
| `setInstanceUrl(instanceUrl: String)` | `LookerDataSourceSpecBuilder` | Sets the instance URL for Looker. `instanceUrl` is the URL of the Looker instance. |
| `setModelName(modelName: String)` | `LookerDataSourceSpecBuilder` | Sets the Looker model name in the Looker instance. `modelName` is the model name in the Looker instance. |
| `setParameterFromCell(parameterName: String, sourceCell: String)` | `LookerDataSourceSpecBuilder` | Adds a parameter, or if the parameter with the name exists, updates its source cell for data source spec builders of type `DataSourceType.BIGQUERY`. This method is only available for BigQuery data sources. `parameterName` is the parameter name; `sourceCell` is the source cell, as specified in A1 notation. |

## Code Samples

```javascript
const lookerDataSourceSpecBuilder =
    SpreadsheetApp.newDataSourceSpec().asLooker();
const lookerSpec = lookerDataSourceSpecBuilder.setExploreName('my explore name')
                       .setInstanceUrl('my instance url')
                       .setModelName('my model name')
                       .build();
```

```javascript
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);
const spec = ss.getDataSources()[0].getSpec();
const newSpec = spec.copy();
```

```javascript
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);
const lookerDataSourceSpec = ss.getDataSources()[0].getSpec().asLooker();
const exploreName = lookerDataSourceSpec.getExploreName();
Logger.log(exploreName);
```

```javascript
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);
const lookerDataSourceSpec = ss.getDataSources()[0].getSpec().asLooker();
const instanceUrl = lookerDataSourceSpec.getInstanceUrl();
Logger.log(instanceUrl);
```

```javascript
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);
const lookerDataSourceSpec = ss.getDataSources()[0].getSpec().asLooker();
const modelName = lookerDataSourceSpec.getModelName();
Logger.log(modelName);
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

```javascript
const specBuilder = SpreadsheetApp.newDataSourceSpec();
specBuilder.removeAllParameters();
```

```javascript
const specBuilder = SpreadsheetApp.newDataSourceSpec();
specBuilder.removeParameter('x');
```

```javascript
const specBuilder = SpreadsheetApp.newDataSourceSpec().asBigQuery();
specBuilder.setParameterFromCell('x', 'A1');
const bigQuerySpec = specBuilder.build();
```
