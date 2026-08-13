# Advanced Chat Service

Source: https://developers.google.com/apps-script/advanced/chat

## Overview

The Advanced Chat Service enables Apps Script developers to integrate Google Chat API functionality, allowing scripts to manage Chat spaces, members, and messages with text, cards, attachments, and reactions.

## Key Requirements

Before using this service, you need:
- A Google Chat app configured in Google Cloud Console
- A standard Google Cloud project (not the default Apps Script project)
- Proper authentication setup (user or service account based on your use case)

## Enabling the Service

This is an advanced service requiring explicit activation. Access it through the Apps Script editor's advanced services menu and enable the Chat API.

## Authorization Scopes

Unlike some services, Apps Script cannot automatically determine Chat service scopes. You must manually add required scopes to your project's `appsscript.json` manifest file:

```json
"oauthScopes": [
  "https://www.googleapis.com/auth/chat.messages.create"
]
```

Common scopes include:
- `chat.messages.create` - Post messages
- `chat.spaces.readonly` - Read space information
- `chat.spaces.create` - Create new spaces
- `chat.memberships.readonly` - View space members
- `chat.messages.readonly` - Read messages

## Sample Implementation

**Post a message with user credentials:**

```javascript
function postMessageWithUserCredentials(spaceName) {
  try {
    const message = { text: "Hello world!" };
    Chat.Spaces.Messages.create(message, spaceName);
  } catch (err) {
    console.log("Failed to create message with error %s", err.message);
  }
}
```

**Get space information:**

```javascript
function getSpace(spaceName) {
  try {
    const space = Chat.Spaces.get(spaceName);
    console.log("Space display name: %s", space.displayName);
  } catch (err) {
    console.log("Failed to get space with error %s", err.message);
  }
}
```

## Limitations

The Advanced Chat Service does not support:
- The Chat API `media.download` method
- Developer Preview methods

Use `UrlFetchApp` as an alternative for these operations.
</content>
