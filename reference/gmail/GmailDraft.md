# GmailDraft

A user-created draft message in a user's Gmail account.

A user-created draft message in a user's Gmail account. Users can perform various actions including deleting, sending, and updating content. Users can retrieve information such as draft ID and underlying GmailMessage. Updating a draft allows replacing contents with new recipient, subject, body, attachments, and HTML body options.

## Methods

### deleteDraft()
**Return type:** `void`

Deletes this draft message.

```javascript
const draft = GmailApp.getDrafts()[0];
draft.deleteDraft();
// draft.getMessage() would now throw an exception
```

### getId()
**Return type:** `String`

Gets the ID of this draft message.

```javascript
const draft = GmailApp.getDrafts()[0];
const draftId = draft.getId();
const draftById = GmailApp.getDraft(draftId);
Logger.log(
    draft.getMessage().getSubject() === draftById.getMessage().getSubject(),
);
```

### getMessage()
**Return type:** `GmailMessage`

Returns a GmailMessage representing this draft.

```javascript
const draft = GmailApp.getDrafts()[0];
Logger.log(draft.getMessage().getSubject());
```

### getMessageId()
**Return type:** `String`

Returns the ID of the GmailMessage representing this draft.

```javascript
const draft = GmailApp.getDrafts()[0];
const messageId = draft.getMessageId();
Logger.log(messageId === draft.getMessage().getId());
```

### send()
**Return type:** `GmailMessage`

Sends this draft email message. The size of the email (including headers) is quota limited.

```javascript
const draft = GmailApp.getDrafts()[0];
const message = draft.send();
Logger.log(message.getDate());
```

### update(recipient, subject, body)
**Parameters:** `recipient` (String), `subject` (String), `body` (String)
**Return type:** `GmailDraft`

Replaces the contents of this draft message. The size of the email (including headers) is quota limited.

```javascript
const draft = GmailApp.getDrafts()[0];
const now = new Date();
draft.update(
    'mike@example.com',
    'current time',
    `The time is: ${now.toString()}`,
);
```

### update(recipient, subject, body, options)
**Parameters:** `recipient` (String), `subject` (String), `body` (String), `options` (Object)
**Return type:** `GmailDraft`

Replaces the contents of this draft message, using optional arguments. The email can contain plain text or an HTML body.

Advanced parameters (options object): `attachments`, `bcc`, `cc`, `from`, `htmlBody`, `inlineImages`, `name`, `replyTo`

```javascript
const draft = GmailApp.getDrafts()[0];
const file = DriveApp.getFileById('1234567890abcdefghijklmnopqrstuvwxyz');
draft.update(
    'mike@example.com',
    'Attachment example',
    'Please see attached file.',
    {
      attachments: [file.getAs(MimeType.PDF)],
      name: 'Automatic Emailer Script',
    },
);
```
