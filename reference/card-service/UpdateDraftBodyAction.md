# UpdateDraftBodyAction

Updates the email draft body.

UpdateDraftBodyAction updates the email draft body.

## Methods

### addUpdateContent(content: String, contentType: ContentType): UpdateDraftBodyAction

Adds the specified content to the draft body. The type of the `content` is specified by `ContentType`.

Parameters:
- `content` (String): The content to insert to the email draft.
- `contentType` (ContentType): The content type of the content to be inserted.

Returns: This object, for chaining.

### setUpdateType(updateType: UpdateDraftBodyType): UpdateDraftBodyAction

Sets the `UpdateDraftBodyType` of this update action on the draft body. For example, inserting content at the start, end, or cursor position of the draft body.

Parameters:
- `updateType` (UpdateDraftBodyType): The type of update to be performed on an email draft.

Returns: This object, for chaining.
