# Send Google Chat messages

Google Chat apps can send and update messages in response to user interactions.

## Key Implementation Details

### Message composition

Apps can include text (with hyperlinks, @mentions, emoji), cards, and interactive widgets.

### Response triggers

Apps respond to message triggers, "added to space" events, and button clicks.

### Two sending methods

Either return `DataActions` with `CreateMessageAction` for immediate replies, or call the Google Chat API for advanced scenarios.

### Reply with a Message

Chat apps return this structure to send messages:

```json
{ "hostAppDataAction": { "chatDataAction": { "createMessageAction": { "message": MESSAGE }}}}
```

### Update a Message

To modify previously sent messages:

```json
{ "hostAppDataAction": { "chatDataAction": { "updateMessageAction": { "message": MESSAGE }}}}
```

## When to Use Google Chat API

Rather than add-on actions, use the Chat API for:

- Scheduled messages or notifications about external resource changes
- Responses exceeding 30 seconds
- Messages outside the interaction space
- Messages on behalf of users

## Prerequisites

Developers need either Node.js or Apps Script, plus a Google Workspace add-on extending Google Chat. The guide provides code examples in Node.js, Python, Java, and Apps Script.
