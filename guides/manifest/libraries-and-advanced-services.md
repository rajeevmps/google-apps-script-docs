# Libraries and advanced services dependencies manifest resource

## Page Summary

- Dependencies in a script manifest configure the libraries and advanced services the script uses.
- The `dependencies` JSON includes `enabledAdvancedServices` and `libraries`.
- `EnabledAdvancedService` configuration includes the service identifier, user symbol, and version.
- `Library` configuration includes development mode, library ID, user symbol, and version.

## Dependencies

The top-level of the dependency manifest configuration.

### JSON representation

```json
{
  "enabledAdvancedServices": [
    {
      object (EnabledAdvancedService)
    }
  ],
  "libraries": [
    {
      object (Library)
    }
  ]
}
```

### Fields

| Field | Type | Description |
|-------|------|-------------|
| `enabledAdvancedServices[]` | `object (EnabledAdvancedService)` | The list of advanced services enabled for the script project. |
| `libraries[]` | `object (Library)` | The list of libraries used by the script project. |

## EnabledAdvancedService

The configuration of an enabled advanced service.

### JSON representation

```json
{
  "serviceId": string,
  "userSymbol": string,
  "version": string
}
```

### Fields

| Field | Type | Description |
|-------|------|-------------|
| `serviceId` | `string` | The service identifier shown in the API discovery document (for example, "drive"). |
| `userSymbol` | `string` | The identifier used to refer to this service in the Apps Script project code. |
| `version` | `string` | The enabled service version (for example, "v1"). |

## Library

The configuration of an imported library.

### JSON representation

```json
{
  "developmentMode": boolean,
  "libraryId": string,
  "userSymbol": string,
  "version": string
}
```

### Fields

| Field | Type | Description |
|-------|------|-------------|
| `developmentMode` | `boolean` | If `true`, the script ignores `version` and uses the current library project code. |
| `libraryId` | `string` | The script ID of the library project. You can find the script ID in the project URL or by selecting **File** > **Project properties**. |
| `userSymbol` | `string` | The label used in the script project code to refer to this library. |
| `version` | `string` | The library version used by the script. This is a version number or `stable`. |

Source: https://developers.google.com/apps-script/manifest/dependencies
