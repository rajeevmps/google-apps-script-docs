# AuthorizationException

An error used to trigger an authorization card for the user.

AuthorizationException is an error used to trigger an authorization card for the user. It allows developers to request user authorization by displaying a card with a custom authorization URL and resource name.

```javascript
CardService.newAuthorizationException()
    .setAuthorizationUrl('http://auth.com/')
    .setResourceDisplayName('Example Resource')
    .throwException();
```

## Methods

### printJson(): String

Prints the JSON representation of this object. This is for debugging only.

### setAuthorizationUrl(authUrl: String): AuthorizationException

Sets the authorization URL that user is taken to from the authorization prompt. Required.

Parameters:
- `authUrl` (String): The authorization URL to set.

Returns: This object, for chaining.

### setCustomUiCallback(callback: String): AuthorizationException

The name of a function to call to generate a custom authorization prompt. Optional.

Parameters:
- `callback` (String): The name of the function that generates a custom authorization prompt.

Returns: This object, for chaining.

### setResourceDisplayName(name: String): AuthorizationException

Sets the name that is displayed to the user when asking for authorization. Required.

Parameters:
- `name` (String): The display name.

Returns: This object, for chaining.

### throwException(): void

Triggers this exception to be thrown.
