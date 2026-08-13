# SetCredentialsResponse

Builder to create a setCredentials() response for your script project.

The `SetCredentialsResponse` is a builder used to create a response for the `setCredentials()` function in a script project within Google Data Studio connectors.

## Methods

### build()

**Signature:** `build(): Object`

**Description:** Validates this object and returns it in the format needed by Data Studio. Returns the validated `SetCredentialsResponse` object.

### printJson()

**Signature:** `printJson(): String`

**Description:** Prints the JSON representation of this object. This is for debugging only.

### setIsValid(isValid)

**Signature:** `setIsValid(isValid: Boolean): SetCredentialsResponse`

**Description:** Sets the valid status of this `SetCredentialsResponse`. Set to `true` if the credentials provided in the request were valid, `false` otherwise. Returns this builder for method chaining.

## Code Sample

```javascript
const communityConnector = DataStudioApp.createCommunityConnector();

function setCredentials(request) {
  const isValid = validateCredentials(request);

  if (isValid) {
    // store the credentials somewhere.
  }

  return communityConnector.newSetCredentialsResponse()
    .setIsValid(isValid)
    .build();
}

function validateCredentials(request) {
  // ...
}
```
