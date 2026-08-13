# AuthorizationAction

An authorization action that sends the user to an authorization URL.

An authorization action that will send the user to the AuthorizationUrl when clicked.

```javascript
CardService.newAuthorizationAction().setAuthorizationUrl('http://google.com/');
```

## Methods

### setAuthorizationUrl(authorizationUrl: String): AuthorizationAction

Sets the authorization URL that user is taken to from the authorization prompt. Required.

Parameters:
- `authorizationUrl` (String): The authorization URL to set.

Returns: This object, for chaining.
