# Admin SDK Groups Migration Service

Source: https://developers.google.com/apps-script/advanced/admin-sdk-groups-migration

## Overview

The Admin SDK Groups Migration service in Apps Script enables administrators to migrate emails from public folders and distribution lists to Google Groups discussion archives. According to the documentation, "This API gives administrators of Google Workspace domains (including resellers) the ability to migrate emails from public folders and distribution lists to Google Groups discussion archives."

## Enabling the Service

This is an advanced service that must be enabled before use, activated through the advanced services interface in Apps Script.

## Reference Documentation

Detailed information is available in the [Admin SDK Groups Migration API reference documentation](https://developers.google.com/admin-sdk/groups-migration/v1/reference). The service uses the same objects, methods, and parameters as the public API. (External link — not scraped.)

For support issues, see the [Admin SDK Groups Migration support guide](https://developers.google.com/admin-sdk/groups-migration/support). (External link — not scraped.)

## Sample Code

The provided example demonstrates migrating emails from Gmail to a Google Group:

```javascript
/**
 * Gets three RFC822 formatted messages from the each of the latest three
 * threads in the user's Gmail inbox, creates a blob from the email content
 * (including attachments), and inserts it in a Google Group in the domain.
 */
function migrateMessages() {
  // TODO (developer) - Replace groupId value with yours
  const groupId = "exampleGroup@example.com";
  const messagesToMigrate = getRecentMessagesContent();
  for (const messageContent of messagesToMigrate) {
    const contentBlob = Utilities.newBlob(messageContent, "message/rfc822");
    AdminGroupsMigration.Archive.insert(groupId, contentBlob);
  }
}

/**
 * Gets a list of recent messages' content from the user's Gmail account.
 * By default, fetches 3 messages from the latest 3 threads.
 *
 * @return {Array} the messages' content.
 */
function getRecentMessagesContent() {
  const NUM_THREADS = 3;
  const NUM_MESSAGES = 3;
  const threads = GmailApp.getInboxThreads(0, NUM_THREADS);
  const messages = GmailApp.getMessagesForThreads(threads);
  const messagesContent = [];
  for (let i = 0; i < messages.length; i++) {
    for (let j = 0; j < NUM_MESSAGES; j++) {
      const message = messages[i][j];
      if (message) {
        messagesContent.push(message.getRawContent());
      }
    }
  }
  return messagesContent;
}
```
</content>
