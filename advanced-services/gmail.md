# Advanced Gmail Service

Source: https://developers.google.com/apps-script/advanced/gmail

## Overview

The Advanced Gmail Service enables developers to leverage the Gmail API within Google Apps Script to manage threads, messages, and labels. While the built-in Gmail service often suffices, this advanced option provides "extra features and access to more detailed information about Gmail content."

## Key Characteristics

- **Purpose**: Find and modify Gmail threads, messages, and labels programmatically
- **Requirement**: Must be enabled before use as an advanced service
- **API Version**: Uses Gmail API v1
- **Performance Note**: List requests return limited data; follow-up `get` requests retrieve full details

## Code Examples

### List Label Information
```javascript
function listLabelInfo() {
  try {
    const response = Gmail.Users.Labels.list("me");
    for (let i = 0; i < response.labels.length; i++) {
      const label = response.labels[i];
      console.log(JSON.stringify(label));
    }
  } catch (err) {
    console.log(err);
  }
}
```

### List Inbox Snippets
```javascript
function listInboxSnippets() {
  try {
    let pageToken;
    do {
      const threadList = Gmail.Users.Threads.list("me", {
        q: "label:inbox",
        pageToken: pageToken,
      });
      if (threadList.threads && threadList.threads.length > 0) {
        for (const thread of threadList.threads) {
          console.log(`Snippet: ${thread.snippet}`);
        }
      }
      pageToken = threadList.nextPageToken;
    } while (pageToken);
  } catch (err) {
    console.log(err);
  }
}
```

### List Unread Messages
```javascript
function listMessages() {
  const userId = "me";
  const options = {
    maxResults: 10,
    q: "is:unread",
  };

  try {
    const response = Gmail.Users.Messages.list(userId, options);
    const messages = response.messages;
    console.log("Unread Messages:");

    for (const message of messages) {
      console.log(`- Message ID: ${message.id}`);
    }
  } catch (err) {
    console.log(`Failed with error: ${err.message}`);
  }
}
```

## Resources

- Reference documentation available at Gmail API v1 reference (external — not scraped)
- Support guidance provided through Gmail support guide (external — not scraped)
</content>
