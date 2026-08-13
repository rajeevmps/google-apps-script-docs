# UpdateDraftActionResponse

Represents an action that updates the email draft that the user is currently editing.

Represents an action that updates the email draft that the user is currently editing.

An UpdateDraftActionResponse enables modification of email drafts with capabilities to update recipients (To, Cc, Bcc), subject lines, and body content. Body content can be inserted as immutable or mutable HTML or plain text.

## Methods

### printJson(): String

Prints the JSON representation of this object. This is for debugging only.

```javascript
// Add "To" recipients.
CardService.newUpdateDraftActionResponseBuilder().setUpdateToRecipientsAction(
    CardService.newUpdateToRecipientsAction().addUpdateToRecipients(['joe@example.com', 'wen@example.com']));

// Add "Cc" / "Bcc" recipients using similar patterns.
// setUpdateCcRecipientsAction() and setUpdateBccRecipientsAction()

// Set the subject line.
CardService.newUpdateDraftActionResponseBuilder().setUpdateDraftSubjectAction(
    CardService.newUpdateDraftSubjectAction().addUpdateSubject('example subject'));

// Insert immutable HTML content.
CardService.newUpdateDraftBodyAction().addUpdateContent(
    '<a href="https://www.google.com">Google</a>', CardService.ContentType.IMMUTABLE_HTML);

// Insert mutable HTML content.
CardService.newUpdateDraftBodyAction().addUpdateContent(
    '<a href="https://www.google.com">Google</a>', CardService.ContentType.MUTABLE_HTML);

// Add multiple content types with UpdateDraftBodyType.IN_PLACE_INSERT.
```
