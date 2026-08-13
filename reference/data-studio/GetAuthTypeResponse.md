# GetAuthTypeResponse

Builder to create a getAuthType() response for your script project.

Builder to create a `getAuthType()` response for your script project, used in Data Studio connectors.

## Methods

### build()

**Signature:** `build(): Object`

**Description:** Validates this object and returns it in the format needed by Data Studio.

### printJson()

**Signature:** `printJson(): String`

**Description:** Prints the JSON representation of this object. This is for debugging only.

### setAuthType(authType)

**Signature:** `setAuthType(authType: AuthType): GetAuthTypeResponse`

**Description:** Sets the `AuthType` of the builder. Returns this builder, for chaining.

### setHelpUrl(helpUrl)

**Signature:** `setHelpUrl(helpUrl: String): GetAuthTypeResponse`

**Description:** Sets the help URL of the builder. The help URL is an optional URL the user can visit to get help on setting up auth. This is only supported for `USER_PASS`, `KEY`, and `USER_TOKEN` authTypes. Returns this builder, for chaining.

## Code Sample

```javascript
function getAuthType() {
  const cc = DataStudioApp.createCommunityConnector();
  return cc.newAuthTypeResponse()
      .setAuthType(cc.AuthType.USER_PASS)
      .setHelpUrl('https://www.example.org/connector-auth-help')
      .build();
}
```
