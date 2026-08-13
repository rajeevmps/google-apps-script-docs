# ComposeActionResponse

The response object that may be returned from a callback method for compose action in a Gmail add-on.

The response object that may be returned from a callback method for compose action in a Gmail add-on. This object isn't related to compose actions that are used to extend the compose UI. Rather, this object is a response to an Action that composes draft messages when a specific UI element is selected.

```javascript
const composeActionResponse =
    CardService.newComposeActionResponseBuilder()
        .setGmailDraft(GmailApp.createDraft('recipient', 'subject', 'body'))
        .build();
```

## Methods

### printJson(): String

Prints the JSON representation of this object. This is for debugging only.
