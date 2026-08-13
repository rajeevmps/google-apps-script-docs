# UpdateDraftActionResponseBuilder

A builder for `UpdateDraftActionResponse` objects.

A builder for `UpdateDraftActionResponse` objects.

## Methods

### build()

`build(): UpdateDraftActionResponse`

Builds the current update draft action response and validates it.

**Throws:** Error if the constructed UpdateDraftActionResponse isn't valid.

### setSendStatus(sendStatus)

`setSendStatus(sendStatus: SendStatus): UpdateDraftActionResponseBuilder`

Sets the enum field that determines whether or not the email sends after the update action.

**Parameters**
- `sendStatus` (SendStatus) — The enum that indicates whether or not the email sends after the update action.

**Returns**
- `UpdateDraftActionResponseBuilder` — This object, for chaining.

### setUpdateDraftBccRecipientsAction(updateDraftBccRecipientsAction)

`setUpdateDraftBccRecipientsAction(updateDraftBccRecipientsAction: UpdateDraftBccRecipientsAction): UpdateDraftActionResponseBuilder`

Sets an action that updates the email Bcc recipients of a draft.

**Parameters**
- `updateDraftBccRecipientsAction` (UpdateDraftBccRecipientsAction) — The action that updates the draft Bcc recipients.

**Returns**
- `UpdateDraftActionResponseBuilder` — This object, for chaining.

### setUpdateDraftBodyAction(updateDraftBodyAction)

`setUpdateDraftBodyAction(updateDraftBodyAction: UpdateDraftBodyAction): UpdateDraftActionResponseBuilder`

Set an action that updates the email body of a draft.

**Parameters**
- `updateDraftBodyAction` (UpdateDraftBodyAction) — The action that updates the draft body.

**Returns**
- `UpdateDraftActionResponseBuilder` — This object, for chaining.

### setUpdateDraftCcRecipientsAction(updateDraftCcRecipientsAction)

`setUpdateDraftCcRecipientsAction(updateDraftCcRecipientsAction: UpdateDraftCcRecipientsAction): UpdateDraftActionResponseBuilder`

Sets an action that updates the Cc recipients of a draft.

**Parameters**
- `updateDraftCcRecipientsAction` (UpdateDraftCcRecipientsAction) — The action that updates the draft Cc recipients.

**Returns**
- `UpdateDraftActionResponseBuilder` — This object, for chaining.

### setUpdateDraftSubjectAction(updateDraftSubjectAction)

`setUpdateDraftSubjectAction(updateDraftSubjectAction: UpdateDraftSubjectAction): UpdateDraftActionResponseBuilder`

Sets an action that updates the subject line of a draft.

**Parameters**
- `updateDraftSubjectAction` (UpdateDraftSubjectAction) — The action that updates the subject line.

**Returns**
- `UpdateDraftActionResponseBuilder` — This object, for chaining.

### setUpdateDraftToRecipientsAction(updateDraftToRecipientsAction)

`setUpdateDraftToRecipientsAction(updateDraftToRecipientsAction: UpdateDraftToRecipientsAction): UpdateDraftActionResponseBuilder`

Sets an action that updates the To recipients of a draft.

**Parameters**
- `updateDraftToRecipientsAction` (UpdateDraftToRecipientsAction) — The action that updates the To recipients.

**Returns**
- `UpdateDraftActionResponseBuilder` — This object, for chaining.
