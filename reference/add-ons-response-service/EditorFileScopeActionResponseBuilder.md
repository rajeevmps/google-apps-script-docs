# EditorFileScopeActionResponseBuilder

A builder for `EditorFileScopeActionResponse` objects.

A builder for `EditorFileScopeActionResponse` objects.

## Methods

### build()

`build(): EditorFileScopeActionResponse`

Builds the current Editor action response.

**Returns**
- `EditorFileScopeActionResponse` — A validated `EditorFileScopeActionResponse`.

### requestFileScopeForActiveDocument()

`requestFileScopeForActiveDocument(): EditorFileScopeActionResponseBuilder`

Requests the `drive.file` scope for the current active Editor document.

Note: To call this method, you must add the `drive.file` scope to the add-on's manifest.

**Returns**
- `EditorFileScopeActionResponseBuilder` — This object, for chaining.

## Code Sample

```javascript
// Display a permissions dialog to the user, requesting `drive.file` scope for
// the current document on behalf of this add-on.
AddOnsResponseService.newEditorFileScopeActionResponseBuilder()
    .requestFileScopeForActiveDocument()
    .build();
```
