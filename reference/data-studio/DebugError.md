# DebugError

An error that is only visible to admins of the connector.

An error that is only visible to admins of the connector. This class enables connector administrators to see error messages that regular users cannot access.

## Methods

### printJson()

**Signature:** `printJson(): String`

**Description:** Prints the JSON representation of this object. This is for debugging only.

### setText(text)

**Signature:** `setText(text: String): DebugError`

**Description:** Sets the text of the debug error, which is only shown to admins. Returns this object, for chaining.

### throwException()

**Signature:** `throwException(): void`

**Description:** Triggers this exception to be thrown.

## Code Sample

```javascript
const cc = DataStudioApp.createCommunityConnector();
cc.newDebugError()
  .setText('This is the debug error text.')
  .throwException();
```
