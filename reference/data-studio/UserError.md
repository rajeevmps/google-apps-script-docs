# UserError

An error shown to users of the connector.

A UserError is an error shown to users of the connector. You can set the text of the error shown to users and a different debug text shown only to admins. The `throwException()` method is used to trigger the exception.

## Code Sample

```javascript
const cc = DataStudioApp.createCommunityConnector();
cc.newUserError()
    .setText('This is the debug error text.')
    .setDebugText('This text is only shown to admins.')
    .throwException();
```

## Methods

### printJson()

**Signature:** `printJson(): String`

**Description:** Prints the JSON representation of this object. This is for debugging only.

### setDebugText(text)

**Signature:** `setDebugText(text: String): UserError`

**Description:** Sets the text of the debug error, which is only shown to admins.

### setText(text)

**Signature:** `setText(text: String): UserError`

**Description:** Sets the text of the user error.

### throwException()

**Signature:** `throwException(): void`

**Description:** Triggers this exception to be thrown.
