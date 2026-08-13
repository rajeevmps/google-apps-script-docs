# StateTokenBuilder

Allows scripts to create state tokens that can be used in callback APIs (like OAuth flows).

Allows scripts to create state tokens that can be used in callback APIs (like OAuth flows).

## Methods

### createToken() → String

Constructs an encrypted string representation of the state token.

**Return:** `String` — An encrypted string representing the token.

```javascript
const stateToken = ScriptApp.newStateToken().createToken();
```

### withArgument(name: String, value: String) → StateTokenBuilder

Adds an argument to the token. This method can be called multiple times.

**Parameters:**
- `name` (`String`): The name of the argument.
- `value` (`String`): The value of the argument.

**Return:** `StateTokenBuilder` — The state token builder, for chaining.

```javascript
const stateToken = ScriptApp.newStateToken()
    .withArgument('myField', 'myValue').createToken();
```

### withMethod(method: String) → StateTokenBuilder

Sets a callback function. The default is a function named `callback()`.

**Parameters:**
- `method` (`String`): The name of the callback function, represented as a string without parentheses or arguments.

**Return:** `StateTokenBuilder` — The state token builder, for chaining.

```javascript
const stateToken = ScriptApp.newStateToken()
    .withMethod('myCallback').createToken();
```

### withTimeout(seconds: Integer) → StateTokenBuilder

Sets the duration (in seconds) for which the token is valid. The defaults is 60 seconds; the maximum duration is 3600 seconds (1 hour).

**Parameters:**
- `seconds` (`Integer`): The duration for which the token is valid; the maximum value is `3600`.

**Return:** `StateTokenBuilder` — The state token builder, for chaining.

```javascript
const stateToken = ScriptApp.newStateToken().withTimeout(60).createToken();
```
