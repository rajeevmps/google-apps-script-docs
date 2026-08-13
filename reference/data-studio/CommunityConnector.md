# CommunityConnector

Enables scripts to access builders and utilities for developing Community Connectors for Data Studio.

The `CommunityConnector` class enables scripts to access builders and utilities for developing Community Connectors for Data Studio. It provides references to the `Fields` object and `FieldType` and `AggregationType` enums for field construction.

## Code Sample

```javascript
const cc = DataStudioApp.createCommunityConnector();
const fields = cc.getFields();
fields.newMetric()
    .setAggregation(cc.AggregationType.AVG)
    .setType(cc.FieldType.CURRENCY_USD);
```

## Properties

| Property | Type | Description |
|----------|------|-------------|
| `AggregationType` | `AggregationType` | The `AggregationType` enumeration |
| `AuthType` | `AuthType` | The `AuthType` enumeration |
| `BigQueryParameterType` | `BigQueryParameterType` | The `BigQueryParameterType` enumeration |
| `FieldType` | `FieldType` | The `FieldType` enumeration |

## Methods

### getConfig()

**Signature:** `getConfig(): Config`

**Description:** Returns a `Config` object. Use this object to add configuration entries.

### getFields()

**Signature:** `getFields(): Fields`

**Description:** Returns a `Fields` object. Use this object to add metric and dimension `Field`s.

### newAuthTypeResponse()

**Signature:** `newAuthTypeResponse(): GetAuthTypeResponse`

**Description:** Returns a new `GetAuthTypeResponse` object. Use this object to create a response for the `getAuthType()` function you implement in your script project.

### newBigQueryConfig()

**Signature:** `newBigQueryConfig(): BigQueryConfig`

**Description:** Returns a new `BigQueryConfig` object. Use this object to create a response for the `getData()` function you implement in your script project.

### newDebugError()

**Signature:** `newDebugError(): DebugError`

**Description:** Returns a new `DebugError` object. Use this object to create debug errors.

### newGetDataResponse()

**Signature:** `newGetDataResponse(): GetDataResponse`

**Description:** Returns a new `GetDataResponse` object. Use this object to create a response for the `getData()` function you implement in your script project.

### newGetSchemaResponse()

**Signature:** `newGetSchemaResponse(): GetSchemaResponse`

**Description:** Returns a new `GetSchemaResponse` object. Use this object to create a response for the `getSchema()` function you implement in your script project.

### newSetCredentialsResponse()

**Signature:** `newSetCredentialsResponse(): SetCredentialsResponse`

**Description:** Returns a new `SetCredentialsResponse` object. Use this object to create a response for the `setCredentials()` function you implement in your script project.

### newUserError()

**Signature:** `newUserError(): UserError`

**Description:** Returns a new `UserError` object. Use this object to create user errors.
