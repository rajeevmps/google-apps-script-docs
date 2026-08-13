# DataSourceConfig

A configuration object that helps configure the data sources for a widget.

A configuration object that helps configure the data sources for a widget.

```javascript
const dataSourceConfig = CardService.newDataSourceConfig()
     .setPlatformDataSource(CardService.newPlatformDataSource()
     .setWorkflowDataSource(CardService.WorkflowDataSourceType.USER));
```

## Methods

### setMaxCharactersToDisable(maxCharactersToDisable: Integer): DataSourceConfig

Sets the maximum number of characters the user can enter before this data provider is disabled. Results are not shown if the input exceeds this length.

Parameters:
- `maxCharactersToDisable` (Integer): The maximum number of characters required. A value of 0 means no limit, always enabled.

### setMaxResults(maxResults: Integer): DataSourceConfig

Sets the maximum number of results to return.

Parameters:
- `maxResults` (Integer): The maximum number of results to return.

### setMinCharactersToTrigger(minCharactersToTrigger: Integer): DataSourceConfig

Sets the minimum number of characters the user must enter before this data provider is triggered to return results.

Parameters:
- `minCharactersToTrigger` (Integer): The minimum number of characters required.

### setPlatformDataSource(platformDataSource: PlatformDataSource): DataSourceConfig

Sets the data source to a platform data source.

Parameters:
- `platformDataSource` (PlatformDataSource): A data source that is shared by all Google Workspace applications.

### setRemoteDataSource(action: Action): DataSourceConfig

Sets the data source to a remote data provider.

Parameters:
- `action` (Action): An action that returns data.
