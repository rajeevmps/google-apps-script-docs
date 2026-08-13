# UpdateDraftActionResponseBuilder

A builder for UpdateDraftActionResponse objects.

UpdateDraftActionResponseBuilder is a builder for `UpdateDraftActionResponse` objects. This builder allows setting actions to update the Bcc, body, Cc, subject, and To recipients of an email draft. The `build()` method finalizes and validates the constructed response.

## Methods

### build(): UpdateDraftActionResponse

Builds the current update draft action response and validates it.

Returns: A validated draft action response.

Throws: Error if the constructed UpdateDraftActionResponse isn't valid.

### setUpdateDraftBccRecipientsAction(updateDraftBccRecipientsAction: UpdateDraftBccRecipientsAction): UpdateDraftActionResponseBuilder

Sets an action that updates the email Bcc recipients of a draft.

Parameters:
- `updateDraftBccRecipientsAction` (UpdateDraftBccRecipientsAction): The action that updates the draft Bcc recipients.

Returns: This object, for chaining.

### setUpdateDraftBodyAction(updateDraftBodyAction: UpdateDraftBodyAction): UpdateDraftActionResponseBuilder

Set an action that updates the email body of a draft.

Parameters:
- `updateDraftBodyAction` (UpdateDraftBodyAction): The action that updates the draft body.

Returns: This object, for chaining.

### setUpdateDraftCcRecipientsAction(updateDraftCcRecipientsAction: UpdateDraftCcRecipientsAction): UpdateDraftActionResponseBuilder

Sets an action that updates the Cc recipients of a draft.

Parameters:
- `updateDraftCcRecipientsAction` (UpdateDraftCcRecipientsAction): The action that updates the draft Cc recipients.

Returns: This object, for chaining.

### setUpdateDraftSubjectAction(updateDraftSubjectAction: UpdateDraftSubjectAction): UpdateDraftActionResponseBuilder

Sets an action that updates the subject line of a draft.

Parameters:
- `updateDraftSubjectAction` (UpdateDraftSubjectAction): The action that updates the subject line.

Returns: This object, for chaining.

### setUpdateDraftToRecipientsAction(updateDraftToRecipientsAction: UpdateDraftToRecipientsAction): UpdateDraftActionResponseBuilder

Sets an action that updates the To recipients of a draft.

Parameters:
- `updateDraftToRecipientsAction` (UpdateDraftToRecipientsAction): The action that updates the To recipients.

Returns: This object, for chaining.
