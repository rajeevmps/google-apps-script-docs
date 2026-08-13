# AuthType

An enum that specifies the authentication types available for connector configuration.

An enumeration that specifies the authentication types available for connector configuration. Access via `DataStudioApp.AuthType.PROPERTY_NAME`.

## Properties (Enum Values)

| Property | Description |
|----------|--------------|
| `NONE` | No authorization needed. |
| `OAUTH2` | OAuth2 authorization needed. |
| `USER_PASS` | Username and password credentials needed. |
| `PATH_USER_PASS` | Username, path, and password needed. |
| `PATH_KEY` | Path and key needed. |
| `KEY` | API Key or Token needed. |
| `USER_TOKEN` | Username and token needed. |
