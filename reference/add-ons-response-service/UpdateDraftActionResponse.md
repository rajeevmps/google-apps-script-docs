# UpdateDraftActionResponse

Represents an action that updates the email draft that the user is currently editing.

Represents an action that updates the email draft that the user is currently editing.

## Methods

### printJson()

`printJson(): String`

Prints the JSON representation of this object. This is for debugging only.

## Code Samples

The documentation provides seven code examples demonstrating usage:

1. Inserting To recipients into a draft
2. Inserting Cc recipients into a draft
3. Inserting Bcc recipients into a draft
4. Inserting a subject line into a draft
5. Inserting immutable HTML content (non-editable link) into a draft body
6. Inserting mutable HTML content (editable link) into a draft body
7. Inserting multiple content values of different types at the cursor position

All examples use `AddOnsResponseService.newUpdateDraftActionResponseBuilder()` to construct the response object and call `.build()` to finalize it.
