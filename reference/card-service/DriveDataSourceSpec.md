# DriveDataSourceSpec

Holds a set of DriveItemType objects that are displayed in a row.

Holds a set of `DriveItemType` objects that are displayed in a row.

```javascript
const driveDataSourceSpec =
    CardService.newDriveDataSourceSpec()
     .addItemType(CardService.DriveItemType.DOCUMENTS)
     .addItemType(CardService.DriveItemType.FORMS);
```

## Methods

### addItemType(driveItemType: DriveItemType): DriveDataSourceSpec

Adds a driveItemType to allowed item types list.

Parameters:
- `driveItemType` (DriveItemType): The driveItemType to add.

Return: `DriveDataSourceSpec` — This object, for chaining.
