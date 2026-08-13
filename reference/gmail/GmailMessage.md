# GmailMessage

A message in a user's Gmail account.

A message in a user's Gmail account. The GmailMessage class represents a single email message within a user's Gmail account, offering methods to create draft replies, forward messages, retrieve message details (attachments, recipients, date, sender, subject, body content), check message status (draft, in chats, inbox, priority inbox, trash, starred, unread), and perform actions like marking as read/unread, moving to trash, starring, and refreshing state.

## Methods

### createDraftReply(body)
**Parameters:** `body` (String)
**Return type:** `GmailDraft`

Creates a draft message replying to the sender of this message using the reply-to address. The size of the email (including headers) is quota limited.

```javascript
const firstThread = GmailApp.getInboxThreads(0, 1)[0];
const message = firstThread.getMessages()[0];
message.createDraftReply('Got your message');
```

### createDraftReply(body, options)
**Parameters:** `body` (String), `options` (Object)
**Return type:** `GmailDraft`

Creates a draft message replying to the sender using the reply-to address, with optional arguments. The email can contain both plain text and HTML body.

Advanced parameters (options object): `attachments`, `bcc`, `cc`, `from`, `htmlBody`, `inlineImages`, `name`, `replyTo`, `subject`

```javascript
const firstThread = GmailApp.getInboxThreads(0, 1)[0];
const message = firstThread.getMessages()[0];
message.createDraftReply('incapable of HTML', {
  htmlBody: '<b>some HTML body text</b>',
  cc: 'another@example.com',
});
```

### createDraftReplyAll(body)
**Parameters:** `body` (String)
**Return type:** `GmailDraft`

Creates a draft message replying to the sender using the reply-to address and all recipients of this message. The size of the email (including headers) is quota limited.

```javascript
const firstThread = GmailApp.getInboxThreads(0, 1)[0];
const message = firstThread.getMessages()[0];
message.createDraftReplyAll('Got your message');
```

### createDraftReplyAll(body, options)
**Parameters:** `body` (String), `options` (Object)
**Return type:** `GmailDraft`

Creates a draft message replying to the sender using the reply-to address and all recipients, with optional arguments. The email can contain both plain text and HTML body.

Advanced parameters (options object): `attachments`, `bcc`, `cc`, `from`, `htmlBody`, `inlineImages`, `name`, `replyTo`, `subject`

```javascript
const firstThread = GmailApp.getInboxThreads(0, 1)[0];
const message = firstThread.getMessages()[0];
message.createDraftReplyAll('incapable of HTML', {
  htmlBody: '<b>some HTML body text</b>',
  cc: 'another@example.com',
});
```

### forward(recipient)
**Parameters:** `recipient` (String) — a comma-separated list of email addresses
**Return type:** `GmailMessage`

Forwards this message to new recipients. The size of the email (including headers) is quota limited.

```javascript
const firstThread = GmailApp.getInboxThreads(0, 1)[0];
const message = firstThread.getMessages()[0];
message.forward('recipient1@example.com,recipient2@example.com');
```

### forward(recipient, options)
**Parameters:** `recipient` (String), `options` (Object)
**Return type:** `GmailMessage`

Forwards this message to new recipients, with optional arguments. The email can contain both plain text and HTML body.

Advanced parameters (options object): `attachments`, `bcc`, `cc`, `from`, `htmlBody`, `inlineImages`, `name`, `noReply`, `replyTo`, `subject`

```javascript
const firstThread = GmailApp.getInboxThreads(0, 1)[0];
const message = firstThread.getMessages()[0];
message.forward('recipient1@example.com,recipient2@example.com', {
  cc: 'myboss@example.com',
  bcc: 'mybosses-boss@example.com,vp@example.com',
});
```

### getAttachments()
**Return type:** `GmailAttachment[]`

Gets all the attachments for this message.

### getAttachments(options)
**Parameters:** `options` (Object) — advanced parameters with `includeInlineImages` (Boolean) and `includeAttachments` (Boolean)
**Return type:** `GmailAttachment[]`

Gets all the attachments for this message.

### getBcc()
**Return type:** `String`

Gets the comma-separated recipients bcc'd on this message. This is empty for all received messages, by definition.

```javascript
const thread = GmailApp.getInboxThreads(0, 1)[0];
const message = thread.getMessages()[0];
Logger.log(message.getBcc());
```

### getBody()
**Return type:** `String`

Gets the HTML content of the body of this message.

```javascript
const thread = GmailApp.getInboxThreads(0, 1)[0];
const message = thread.getMessages()[0];
Logger.log(message.getBody());
```

### getCc()
**Return type:** `String`

Gets the comma-separated recipients cc'd on this message.

```javascript
const thread = GmailApp.getInboxThreads(0, 1)[0];
const message = thread.getMessages()[0];
Logger.log(message.getCc());
```

### getDate()
**Return type:** `Date`

Gets the date and time of this message.

```javascript
const thread = GmailApp.getInboxThreads(0, 1)[0];
const message = thread.getMessages()[0];
Logger.log(message.getDate());
```

### getFrom()
**Return type:** `String`

Gets the sender of this message.

```javascript
const thread = GmailApp.getInboxThreads(0, 1)[0];
const message = thread.getMessages()[0];
Logger.log(message.getFrom());
```

### getHeader(name)
**Parameters:** `name` (String) — the name of the RFC header, without the colon separating it from the value
**Return type:** `String`

Gets the value of an RFC 2822 header given the header name.

```javascript
const thread = GmailApp.getInboxThreads(0, 1)[0];
const message = thread.getMessages()[0];
Logger.log(message.getHeader('Message-ID'));
```

### getId()
**Return type:** `String`

Gets the ID of this message.

```javascript
const thread = GmailApp.getInboxThreads(0, 1)[0];
const message = thread.getMessages()[0];
const id = message.getId();
const messageById = GmailApp.getMessageById(id);
```

### getPlainBody()
**Return type:** `String`

Gets the content of the body of this message without HTML formatting.

### getRawContent()
**Return type:** `String`

Gets the raw content of this message.

### getReplyTo()
**Return type:** `String`

Gets the reply-to address of this message (usually the sender).

### getSubject()
**Return type:** `String`

Gets the subject of this message.

### getThread()
**Return type:** `GmailThread`

Gets the thread that contains this message.

### getTo()
**Return type:** `String`

Gets the comma-separated recipients of this message.

### isDraft()
**Return type:** `Boolean`

Gets whether this message is a draft.

### isInChats()
**Return type:** `Boolean`

Gets whether this message is a chat.

### isInInbox()
**Return type:** `Boolean`

Gets whether this message is in the inbox.

### isInPriorityInbox()
**Return type:** `Boolean`

Returns `true` if this message is in the priority inbox; returns `false` otherwise.

### isInTrash()
**Return type:** `Boolean`

Gets whether this message is in the trash.

### isStarred()
**Return type:** `Boolean`

Gets whether this message is starred.

### isUnread()
**Return type:** `Boolean`

Gets whether this message is unread.

### markRead()
**Return type:** `GmailMessage`

Marks the message as read.

### markUnread()
**Return type:** `GmailMessage`

Marks the message as unread.

### moveToTrash()
**Return type:** `GmailMessage`

Moves the message to the trash.

### refresh()
**Return type:** `GmailMessage`

Reloads this message and associated state from Gmail (useful in case the labels, read state, etc., have changed).

### reply(body)
**Parameters:** `body` (String)
**Return type:** `GmailMessage`

Replies to the sender of this message using the reply-to address.

### reply(body, options)
**Parameters:** `body` (String), `options` (Object)
**Return type:** `GmailMessage`

Replies to the sender of this message using the reply-to address, with optional arguments.

### replyAll(body)
**Parameters:** `body` (String)
**Return type:** `GmailMessage`

Replies to the sender using the reply-to address and all recipients of this message.

### replyAll(body, options)
**Parameters:** `body` (String), `options` (Object)
**Return type:** `GmailMessage`

Replies to the sender of this message using the reply-to address and all recipients, with optional arguments.

### star()
**Return type:** `GmailMessage`

Stars the message.

### unstar()
**Return type:** `GmailMessage`

Unstars the message.
