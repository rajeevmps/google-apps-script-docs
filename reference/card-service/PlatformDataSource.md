# PlatformDataSource

Used for populating items in a multiselect menu within a SelectionInput widget.

PlatformDataSource is used for populating items in a multiselect menu within a SelectionInput widget. This feature is exclusively available for Google Chat apps and cannot be used with Google Workspace add-ons. You can set the data source using setCommonDataSource for Google Workspace data or setHostAppDataSource for populating spaces in a multiselect menu.

## Methods

### setCommonDataSource(commonDataSource: CommonDataSource): PlatformDataSource

Sets the data source from Google Workspace.

### setDriveDataSourceSpec(driveDataSourceSpec: DriveDataSourceSpec): PlatformDataSource

Sets the drive data source spec from Google Workspace.

### setHostAppDataSource(hostAppDataSource: HostAppDataSource): PlatformDataSource

Used to populate spaces in multiselect menu.

```javascript
const platformDataSource =
    CardService.newPlatformDataSource().setCommonDataSource(
        CardService.CommonDataSource.USER,
    );

const multiSelect = CardService.newSelectionInput()
                        .setType(CardService.SelectionInputType.MULTI_SELECT)
                        .setFieldName('contacts')
                        .setTitle('Selected contacts')
                        .setMultiSelectMaxSelectedItems(5)
                        .setMultiSelectMinQueryLength(1)
                        .setPlatformDataSource(platformDataSource);
```
