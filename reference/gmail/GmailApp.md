# GmailApp

Provides access to Gmail threads, messages, and labels.

Provides access to Gmail threads, messages, and labels.

All methods require authorization with scope `https://mail.google.com/`.

## Methods

### createDraft(recipient, subject, body)
**Return type:** `GmailDraft`

Creates a draft email message. The size of the email (including headers) is quota limited.

```javascript
const now = new Date();
GmailApp.createDraft(
    'mike@example.com',
    'current time',
    `The time is: ${now.toString()}`,
);
```

### createDraft(recipient, subject, body, options)
**Return type:** `GmailDraft`

Creates a draft email message with optional arguments. The email can contain plain text or an HTML body. The size of the email (including headers, but excluding attachments) is quota limited.

Advanced parameters (options object): `attachments` (BlobSource[]), `bcc` (String), `cc` (String), `from` (String), `htmlBody` (String), `inlineImages` (Object), `name` (String), `replyTo` (String)

```javascript
const file = DriveApp.getFileById('1234567890abcdefghijklmnopqrstuvwxyz');
GmailApp.createDraft(
    'mike@example.com',
    'Attachment example',
    'Please see attached file.',
    {
      attachments: [file.getAs(MimeType.PDF)],
      name: 'Automatic Emailer Script',
    },
);
```

### createLabel(name)
**Return type:** `GmailLabel`

Create a new user label of the given name.

```javascript
Logger.log(`label: ${GmailApp.createLabel('FOO')}`);
```

### deleteLabel(label)
**Return type:** `GmailApp`

Deletes the specified label.

```javascript
const label = GmailApp.getUserLabelByName('FOO');
GmailApp.deleteLabel(label);
```

### getAliases()
**Return type:** `String[]`

Gets a list of the emails that are set up as aliases for this account in Gmail. You can send a message from any of these aliases by using the "from" optional argument.

```javascript
const me = Session.getActiveUser().getEmail();
const aliases = GmailApp.getAliases();
Logger.log(aliases);
if (aliases.length > 0) {
  GmailApp.sendEmail(me, 'From an alias', 'A message from an alias!', {
    from: aliases[0],
  });
} else {
  GmailApp.sendEmail(me, 'No aliases found', 'You have no aliases.');
}
```

### getDraft(draftId)
**Return type:** `GmailDraft`

Retrieve an email message draft by ID. Use this in conjunction with getId() on Gmail drafts.

```javascript
const draft = GmailApp.getDrafts()[0];
const draftId = draft.getId();
const draftById = GmailApp.getDraft(draftId);
Logger.log(
    draft.getMessage().getSubject() === draftById.getMessage().getSubject(),
);
```

### getDraftMessages()
**Return type:** `GmailMessage[]`

Retrieves all draft messages.

```javascript
const drafts = GmailApp.getDraftMessages();
Logger.log(drafts.length);
```

### getDrafts()
**Return type:** `GmailDraft[]`

Gets all Gmail draft messages.

```javascript
const drafts = GmailApp.getDrafts();
for (let i = 0; i < drafts.length; i++) {
  Logger.log(drafts[i].getId());
}
```

### getInboxThreads()
**Return type:** `GmailThread[]`

Retrieves all Inbox threads irrespective of labels. This call will fail when the size of all threads is too large for the system to handle. Where the thread size is unknown, and potentially very large, please use the "paged" call, and specify ranges of the threads to retrieve in each call.

```javascript
const threads = GmailApp.getInboxThreads();
for (let i = 0; i < threads.length; i++) {
  Logger.log(threads[i].getFirstMessageSubject());
}
```

### getInboxThreads(start, max)
**Return type:** `GmailThread[]`

Retrieves a range of Inbox threads irrespective of labels.

```javascript
const threads = GmailApp.getInboxThreads(0, 50);
for (let i = 0; i < threads.length; i++) {
  Logger.log(threads[i].getFirstMessageSubject());
}
```

### getInboxUnreadCount()
**Return type:** `Integer`

Gets the number of unread threads in the inbox.

```javascript
Logger.log(`Messages unread in inbox: ${GmailApp.getInboxUnreadCount()}`);
```

### getMessageById(id)
**Return type:** `GmailMessage`

Gets a message by ID. Use this in conjunction with getId() on Gmail messages.

```javascript
const message = GmailApp.getInboxThreads(0, 1)[0].getMessages()[0];
const messageId = message.getId();
const messageById = GmailApp.getMessageById(messageId);
Logger.log(message.getSubject() === messageById.getSubject());
```

### getMessagesForThread(thread)
**Parameters:** `thread` (GmailThread)
**Return type:** `GmailMessage[]`

Retrieve all messages in the specified thread.

### getMessagesForThreads(threads)
**Parameters:** `threads` (GmailThread[])
**Return type:** `GmailMessage[][]`

Retrieve all messages in the specified threads.

### getPriorityInboxThreads()
**Return type:** `GmailThread[]`

Retrieves all Priority Inbox threads irrespective of labels.

### getPriorityInboxThreads(start, max)
**Return type:** `GmailThread[]`

Retrieves a range of Priority Inbox threads irrespective of labels.

### getPriorityInboxUnreadCount()
**Return type:** `Integer`

Gets the number of unread threads in the Priority Inbox.

### getSpamThreads()
**Return type:** `GmailThread[]`

Retrieves all spam threads irrespective of labels.

### getSpamThreads(start, max)
**Return type:** `GmailThread[]`

Retrieves a range of spam threads irrespective of labels.

### getSpamUnreadCount()
**Return type:** `Integer`

Gets the number of unread threads that are spam.

### getStarredThreads()
**Return type:** `GmailThread[]`

Retrieves all starred threads irrespective of labels.

### getStarredThreads(start, max)
**Return type:** `GmailThread[]`

Retrieves a range of starred threads irrespective of labels.

### getStarredUnreadCount()
**Return type:** `Integer`

Gets the number of unread threads that are starred.

### getThreadById(id)
**Return type:** `GmailThread|null`

Gets a thread by ID.

### getTrashThreads()
**Return type:** `GmailThread[]`

Retrieves all trash threads irrespective of labels.

### getTrashThreads(start, max)
**Return type:** `GmailThread[]`

Retrieves a range of trash threads irrespective of labels.

### getUserLabelByName(name)
**Return type:** `GmailLabel`

Retrieves a label given the label name.

### getUserLabels()
**Return type:** `GmailLabel[]`

Retrieves a list of user-created labels.

### markMessageRead(message)
**Return type:** `GmailApp`

Marks this message read and forces the message to refresh.

### markMessageUnread(message)
**Return type:** `GmailApp`

Marks this message unread and forces the message to refresh.

### markMessagesRead(messages)
**Return type:** `GmailApp`

Marks these messages read and forces the messages to refresh.

### markMessagesUnread(messages)
**Return type:** `GmailApp`

Marks these messages unread and forces the messages to refresh.

### markThreadImportant(thread)
**Return type:** `GmailApp`

Marks this thread as important and forces the thread to refresh.

### markThreadRead(thread)
**Return type:** `GmailApp`

Marks this thread as read and forces the thread to refresh.

### markThreadUnimportant(thread)
**Return type:** `GmailApp`

Marks this thread as unimportant and forces the thread to refresh.

### markThreadUnread(thread)
**Return type:** `GmailApp`

Marks this thread unread and forces the thread to refresh.

### markThreadsImportant(threads)
**Return type:** `GmailApp`

Marks these threads as important and forces the threads to refresh.

### markThreadsRead(threads)
**Return type:** `GmailApp`

Marks these threads as read and forces the threads to refresh.

### markThreadsUnimportant(threads)
**Return type:** `GmailApp`

Marks these threads as unimportant and forces the threads to refresh.

### markThreadsUnread(threads)
**Return type:** `GmailApp`

Marks these threads as unread and forces the threads to refresh.

### moveMessageToTrash(message)
**Return type:** `GmailApp`

Moves the message to the trash and forces the message to refresh.

### moveMessagesToTrash(messages)
**Return type:** `GmailApp`

Moves the specified messages to the trash and forces the messages to refresh.

### moveThreadToArchive(thread)
**Return type:** `GmailApp`

Moves this thread to the archive and forces the thread to refresh.

### moveThreadToInbox(thread)
**Return type:** `GmailApp`

Moves this thread to the inbox and forces the thread to refresh.

### moveThreadToSpam(thread)
**Return type:** `GmailApp`

Moves this thread to spam and forces the thread to refresh.

### moveThreadToTrash(thread)
**Return type:** `GmailApp`

Moves this thread to the trash and forces the thread to refresh.

### moveThreadsToArchive(threads)
**Return type:** `GmailApp`

Moves these threads to the archive and forces the threads to refresh.

### moveThreadsToInbox(threads)
**Return type:** `GmailApp`

Moves these threads to the inbox and forces the threads to refresh.

### moveThreadsToSpam(threads)
**Return type:** `GmailApp`

Moves these threads to spam and forces the threads to refresh.

### moveThreadsToTrash(threads)
**Return type:** `GmailApp`

Moves these threads to the trash and forces the threads to refresh.

### refreshMessage(message)
**Return type:** `GmailApp`

Reloads the message and associated state from Gmail (useful in case the labels, read state, etc., have changed).

### refreshMessages(messages)
**Return type:** `GmailApp`

Reloads the messages and associated state from Gmail (useful in case the labels, read state, etc., have changed).

### refreshThread(thread)
**Return type:** `GmailApp`

Reloads the thread and associated state from Gmail (useful in case the labels, read state, etc., have changed).

### refreshThreads(threads)
**Return type:** `GmailApp`

Reloads the threads and associated state from Gmail (useful in case the labels, read state, etc., have changed).

### search(query)
**Return type:** `GmailThread[]`

Search Gmail with the given query.

### search(query, start, max)
**Return type:** `GmailThread[]`

Search Gmail with the given query.

### sendEmail(recipient, subject, body)
**Return type:** `GmailApp`

Sends an email message.

### sendEmail(recipient, subject, body, options)
**Return type:** `GmailApp`

Sends an email message with optional arguments.

### setCurrentMessageAccessToken(accessToken)
**Return type:** `void`

Sets the current message access token that enables the script to access the current GmailMessage properties.

### starMessage(message)
**Return type:** `GmailApp`

Adds a star to this message and forces the message to refresh.

### starMessages(messages)
**Return type:** `GmailApp`

Adds stars to these messages and forces the messages to refresh.

### unstarMessage(message)
**Return type:** `GmailApp`

Removes a star from this message and forces the message to refresh.

### unstarMessages(messages)
**Return type:** `GmailApp`

Removes stars from these messages and forces the messages to refresh.

### getChatThreads() — Deprecated
**Return type:** `GmailThread[]`

Gets all classic Google Hangouts threads and Google Chat threads until Google switches all users of classic Hangouts to Chat later this year.

### getChatThreads(start, max) — Deprecated
**Return type:** `GmailThread[]`

Gets a range of classic Google Hangouts threads and Google Chat threads until Google switches all users of classic Hangouts to Chat later this year.
