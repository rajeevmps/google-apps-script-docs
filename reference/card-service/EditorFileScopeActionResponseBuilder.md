# EditorFileScopeActionResponseBuilder

A builder for EditorFileScopeActionResponse objects.

The `EditorFileScopeActionResponseBuilder` is used to build `EditorFileScopeActionResponse` objects. The `build()` method constructs the `EditorFileScopeActionResponse`. The `requestFileScopeForActiveDocument()` method requests the `drive.file` scope for the active Editor document. Requesting the `drive.file` scope requires adding it to the add-on's manifest.

## Methods

### build(): EditorFileScopeActionResponse

Builds the current Editor action response.

Returns: A validated `EditorFileScopeActionResponse`.

### requestFileScopeForActiveDocument(): EditorFileScopeActionResponseBuilder

Requests the `drive.file` scope for the current active Editor document. To call this method, you must add the `drive.file` scope to the add-on's manifest.

Returns: This object, for chaining.

```javascript
CardService.newEditorFileScopeActionResponseBuilder()
    .requestFileScopeForActiveDocument()
    .build();
```
