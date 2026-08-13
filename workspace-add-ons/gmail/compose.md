# Compose draft messages

Note: The techniques described in this guide are primarily for creating new draft messages in response to user interactions in a message UI. If you want your add-on to alter a draft the user is currently viewing, extend the compose UI instead.

In a add-on you can create widgets that have linked actions. You can use an action to compose new email drafts, optionally filling them using information entered into the add-on UI or information from an open message. For example, you can have a button in your add-on's message UI that creates a reply to the currently opened message prepopulated with information from the add-on.

When an action that builds messages is triggered, Gmail executes a callback function to build and return the draft. Gmail then displays that draft in its UI in a standard email compose window, which the user can then edit and send as needed.

## Configure an action to build a draft message

To configure a widget to start a draft-building action when selected, you must do the following:

1. Make sure your manifest includes the `action.compose` scope:

   `https://www.googleapis.com/auth/gmail.addons.current.action.compose`

   You can use more a permissive scope instead, but should only do so if that scope is absolutely necessary.

2. Create an `Action` object and associate it with a callback function you define.

3. Call the widget's `setComposeAction` widget handler function, providing it the `Action` object and specifying the `ComposeEmailType`.

4. Implement the callback function that executes the draft-building action. This function is given an event object as an argument. The callback function must do the following:

   1. Create a `GmailDraft` object.
   2. Build a `ComposeActionResponse` object using the `ComposeActionResponseBuilder` class and the `GmailDraft` object.
   3. Return the built `ComposeActionResponse`.

You can prefill the `GmailDraft` you create in the callback function with recipients, a subject, a message body, and attachments. To fill in the draft, data can come from any source, but typically it derives from information provided to the add-on itself, information in the open message, or information gathered from a third-party service. The event object passed to the callback function contains the open message ID and other add-on information you can use to prefill the draft.

You can create the draft as a new standalone message or a reply to an existing message. This is controlled by the `ComposeEmailType` enum given to the `setComposeAction`. You can create reply drafts as single replies or 'reply-all' messages.

### Standalone drafts

A standalone draft starts a new thread and isn't a reply to any existing message. You can create a standalone draft with one of the following Gmail service functions:

- `GmailApp.createDraft(recipient, subject, body)`
- `GmailApp.createDraft(recipient, subject, body, options)`

### Reply drafts

A reply draft is part of an existing message thread. Reply drafts are either single replies that only get sent to the sender of a message or "reply all" drafts that get sent to everyone who received that message. You can create a reply draft with one of these Gmail service functions:

- `GmailMessage.createDraftReply(body)`
- `GmailMessage.createDraftReply(body, options)`
- `GmailMessage.createDraftReplyAll(body)`
- `GmailMessage.createDraftReplyAll(body, options)`
- `GmailThread.createDraftReply(body)`
- `GmailThread.createDraftReply(body, options)`
- `GmailThread.createDraftReplyAll(body)`
- `GmailThread.createDraftReplyAll(body, options)`

## Example

The following code snippet shows how to assign an action that builds a reply draft to a button.

```javascript
var composeAction = CardService.newAction()
    .setFunctionName('createReplyDraft');
var composeButton = CardService.newTextButton()
    .setText('Compose Reply')
    .setComposeAction(
        composeAction,
        CardService.ComposedEmailType.REPLY_AS_DRAFT);

// ...

/**
 *  Creates a draft email (with an attachment and inline image)
 *  as a reply to an existing message.
 *  @param {Object} e An event object passed by the action.
 *  @return {ComposeActionResponse}
 */
function createReplyDraft(e) {
  // Activate temporary Gmail scopes, in this case to allow
  // a reply to be drafted.
  var accessToken = e.gmail.accessToken;
  GmailApp.setCurrentMessageAccessToken(accessToken);

  // Creates a draft reply.
  var messageId = e.gmail.messageId;
  var message = GmailApp.getMessageById(messageId);
  var draft = message.createDraftReply('',
      {
          htmlBody: "Kitten! <img src='cid:kitten'/>",
          attachments: [
            UrlFetchApp.fetch('https://example.com/images/myDog.jpg')
                .getBlob()
          ],
          inlineImages: {
            "kitten": UrlFetchApp.fetch('https://example.com/images/myKitten.jpg')
                          .getBlob()
          }
      }
  );

  // Return a built draft response. This causes Gmail to present a
  // compose window to the user, pre-filled with the content previously
  // specified.
  return CardService.newComposeActionResponseBuilder()
      .setGmailDraft(draft).build();
}
```
