# GmailThread

A thread in a user's Gmail account.

A thread in a user's Gmail account that enables developers to interact with Gmail conversation threads. The class provides methods to manage labels, create replies, retrieve thread information, and check thread status across various categories like inbox, spam, and trash.

## Methods

### addLabel(label)
**Parameters:** `label` (GmailLabel)
**Return type:** `GmailThread`

Adds a specified label to the thread, useful for organizing and categorizing conversations.

### createDraftReply(body)
**Parameters:** `body` (String)
**Return type:** `GmailDraft`

Generates a draft message responding to the last message sender using the reply-to address.

### createDraftReply(body, options)
**Parameters:** `body` (String), `options` (Object)
**Return type:** `GmailDraft`

Creates a draft reply with optional parameters including attachments, CC/BCC recipients, HTML body, inline images, sender name, reply-to address, and subject line (max 250 characters).

### createDraftReplyAll(body)
**Parameters:** `body` (String)
**Return type:** `GmailDraft`

Generates a draft message replying to all recipients of the last message in the thread.

### createDraftReplyAll(body, options)
**Parameters:** `body` (String), `options` (Object)
**Return type:** `GmailDraft`

Creates a draft reply-all with advanced options for attachments, recipients, HTML formatting, and subject specification.

### getFirstMessageSubject()
**Return type:** `String`

Retrieves the subject line from the thread's initial message.

### getId()
**Return type:** `String`

Obtains the thread's unique identifier for reference purposes.

### getLabels()
**Return type:** `GmailLabel[]`

Returns an array of user-created labels associated with the thread.

### getLastMessageDate()
**Return type:** `Date`

Fetches the timestamp of the thread's most recent message.

### getMessageCount()
**Return type:** `Integer`

Returns the total number of messages contained in the thread.

### getMessages()
**Return type:** `GmailMessage[]`

Retrieves an array of all Gmail messages within the thread.

### getPermalink()
**Return type:** `String`

Obtains a permalink to the thread (compatible with classic Gmail interface only).

### hasStarredMessages()
**Return type:** `Boolean`

Checks whether any messages in the thread have been starred.

### isImportant()
**Return type:** `Boolean`

Determines if the thread is marked as important.

### isInChats()
**Return type:** `Boolean`

Checks if the thread is labeled as a chat conversation.

### isInInbox()
**Return type:** `Boolean`

Verifies whether the thread resides in the inbox folder.

### isInPriorityInbox()
**Return type:** `Boolean`

Determines if the thread appears in the priority inbox section.

### isInSpam()
**Return type:** `Boolean`

Checks if the thread has been marked as spam.

### isInTrash()
**Return type:** `Boolean`

Verifies whether the thread is in the trash folder.

### isUnread()
**Return type:** `Boolean`

Checks if the thread contains any unread messages.

### markImportant()
**Return type:** `GmailThread`

Marks the thread as important for prioritization.

### markRead()
**Return type:** `GmailThread`

Sets all messages in the thread as read.

### markUnimportant()
**Return type:** `GmailThread`

Removes the important designation from the thread.

### markUnread()
**Return type:** `GmailThread`

Marks the thread as containing unread messages.

### moveToArchive()
**Return type:** `GmailThread`

Relocates the thread to the archive folder.

### moveToInbox()
**Return type:** `GmailThread`

Moves the thread back to the inbox.

### moveToSpam()
**Return type:** `GmailThread`

Transfers the thread to the spam folder.

### moveToTrash()
**Return type:** `GmailThread`

Moves the thread to the trash folder.

### refresh()
**Return type:** `GmailThread`

Reloads thread data from Gmail to reflect label, read status, and other state changes.

### removeLabel(label)
**Parameters:** `label` (GmailLabel)
**Return type:** `GmailThread`

Removes a specified label from the thread.

### reply(body)
**Parameters:** `body` (String)
**Return type:** `GmailThread`

Sends a reply to the last message sender using the replyTo address.

### reply(body, options)
**Parameters:** `body` (String), `options` (Object)
**Return type:** `GmailThread`

Sends a reply with advanced options including attachments, CC/BCC, HTML body, and sender details.

### replyAll(body)
**Parameters:** `body` (String)
**Return type:** `GmailThread`

Sends a reply to the sender and all recipients of the last message.

### replyAll(body, options)
**Parameters:** `body` (String), `options` (Object)
**Return type:** `GmailThread`

Sends a reply-all message with optional advanced parameters for customization.
