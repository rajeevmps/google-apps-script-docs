# ComposeActionResponseBuilder

A builder for ComposeActionResponse objects.

A builder for `ComposeActionResponse` objects.

Note: This object isn't related to **compose actions** that are used to extend the compose UI. Rather, this builder creates responses to an `Action` that composes draft messages when a specific UI element is selected.

## Methods

### build(): ComposeActionResponse

Builds the current compose action response and validates it.

Return: A validated `ComposeActionResponse`.

Throws: if the constructed compose action response isn't valid.

### setGmailDraft(draft: GmailDraft): ComposeActionResponseBuilder

Sets the draft `GmailMessage` created using `GmailMessage.createDraftReply(body)` or similar functions.

Parameters:
- `draft` (GmailDraft): The `GmailDraft` to use.

Return: This object, for chaining.
