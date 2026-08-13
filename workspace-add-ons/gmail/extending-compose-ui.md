# Extend the compose UI with compose actions

In addition to providing a card-based interface when a user is reading a Gmail message, Google Workspace add-ons that extend Gmail can provide another interface when the user is composing new messages or replying to existing ones. This lets add-ons automate the task of composing emails for the user.

## Access the Google Workspace add-on compose UI

There are two ways to view an add-on's compose UI. The first way is to start composing a new draft or reply while the add-on is already open. The second way is to start the add-on while composing a draft.

Either case causes the add-on to execute the corresponding compose trigger function, defined in the add-on manifest. The compose trigger function builds the compose UI for that compose action, which Gmail then displays to the user.

## Build a compose add-on

You can add compose functionality to an add-on by following these general steps:

1. Add the `gmail.composeTrigger` field to the add-on script project manifest and update the manifest scopes to include those required for compose actions.
2. Implement a compose trigger function that builds a compose UI when the trigger fires. Compose trigger functions return either a single `Card` object or an array of `Card` objects that form the compose UI for the compose action.
3. Implement associated callback functions needed to react to the user's compose UI interactions. These functions are not the compose action itself (which only causes the compose UI to appear); rather, these are the individual functions that govern what happens when different elements of the compose UI are selected. For example, a UI card containing a button usually has an associated callback function that executes when a user clicks that button. The callback function for widgets that update the draft message content should return a `UpdateDraftActionResponse` object.

## Compose trigger function

An add-on's compose UI is built the same way as the add-on's message UI—using the Apps Script Card service to construct cards and fill them with widgets.

You must implement the `gmail.composeTrigger.selectActions[].runFunction` that you define in your manifest. The compose trigger function must return either a single `Card` object or an array of `Card` objects that form the compose UI for that action. These functions are very similar to contextual trigger functions and should build cards in the same way.

**Warning:** For security reasons, add-ons can't silently change Google Workspace or third-party file access permissions. For example, an add-on can't silently add email recipients to the set of accounts that can view a Dropbox file. Instead, the add-on must inform users that the permission change is occurring. add-ons that don't inform users of such changes can't pass add-on review.

### Compose trigger event objects

When a compose action is selected, it executes the corresponding compose trigger function and passes the function an event object as a parameter. The event object can carry information about the add-on context and the draft being composed to the trigger function.

See Event object structure for details on how information is arranged in the event object. The information contained in the event object is partially controlled by the value of the `gmail.composeTrigger.draftAccess` manifest field:

- If the `gmail.composeTrigger.draftAccess` manifest field is `NONE` or isn't included, the event object has only minimal information.
- If `gmail.composeTrigger.draftAccess` is set to `METADATA`, the event object passed to the compose trigger function is populated with lists of recipients of the email being composed. Using `METADATA` draft access requires that the add-on manifest include the `https://www.googleapis.com/auth/gmail.addons.current.message.metadata` Gmail scope.

## Insert content into active drafts

Typically a add-on compose UI provides the user options and control that help compose a message. For these use cases, once the user has made selections in the UI the add-on interprets the selections and updates the current working email draft accordingly.

To make it easier to update the current draft email, the Card service has been extended with the following classes:

- `ContentType`—An enum that defines whether to add mutable HTML, immutable HTML (which Gmail users can't edit), or plain text content.
- `UpdateDraftActionResponse`—Represents a response to an action that updates the current draft email.
- `UpdateDraftActionResponseBuilder`—A builder for `UpdateDraftActionResponse` objects.
- `UpdateDraftBodyAction`—Represents an action that updates the body of the current draft email.
- `UpdateDraftBodyType`—An enum that defines how the body is changed.
- `UpdateDraftSubjectAction`—Represents an action that updates the subject field of the current draft email.
- `UpdateDraftToRecipientsAction`—Represents an action that updates the To recipients of the current draft email.
- `UpdateDraftCcRecipientsAction`—Represents an action that updates the Cc recipients of the current draft email.
- `UpdateDraftBccRecipientsAction`—Represents an action that updates the Bcc recipients of the current draft email.

Typically an add-on compose UI includes a 'Save' or 'Insert' widget that a user can click to indicate they are done making selections in the UI and want their choices to be added to the email they are composing. To add this interactivity, the widget should have an associated `Action` object that instructs the add-on to run a specific callback function when the widget is clicked. You must implement these callback functions. Each callback function should return a built `UpdateDraftActionResponse` object that details the changes to make to the current draft email.

### Example 1

The following code snippet shows how to build a compose UI that updates the subject, and the To, Cc, and Bcc recipients of the current email draft.

```javascript
/**
 * Compose trigger function that fires when the compose UI is
 * requested. Builds and returns a compose UI for inserting images.
 *
 * @param {event} e The compose trigger event object. Not used in
 *         this example.
 * @return {Card[]}
 */
function getComposeUI(e) {
  return [buildComposeCard()];
}

/**
 * Build a card to display interactive buttons to allow the user to
 * update the subject, and To, Cc, Bcc recipients.
 *
 * @return {Card}
 */
function buildComposeCard() {

  var card = CardService.newCardBuilder();
  var cardSection = CardService.newCardSection().setHeader('Update email');
  cardSection.addWidget(
      CardService.newTextButton()
          .setText('Update subject')
          .setOnClickAction(CardService.newAction()
              .setFunctionName('applyUpdateSubjectAction')));
  cardSection.addWidget(
      CardService.newTextButton()
          .setText('Update To recipients')
          .setOnClickAction(CardService.newAction()
              .setFunctionName('updateToRecipients')));
  cardSection.addWidget(
      CardService.newTextButton()
          .setText('Update Cc recipients')
          .setOnClickAction(CardService.newAction()
              .setFunctionName('updateCcRecipients')));
  cardSection.addWidget(
      CardService.newTextButton()
          .setText('Update Bcc recipients')
          .setOnClickAction(CardService.newAction()
              .setFunctionName('updateBccRecipients')));
  return card.addSection(cardSection).build();
}

/**
 * Updates the subject field of the current email when the user clicks
 * on "Update subject" in the compose UI.
 *
 * Note: This is not the compose action that builds a compose UI, but
 * rather an action taken when the user interacts with the compose UI.
 *
 * @return {UpdateDraftActionResponse}
 */
function applyUpdateSubjectAction() {
  // Get the new subject field of the email.
  // This function is not shown in this example.
  var subject = getSubject();
  var response = CardService.newUpdateDraftActionResponseBuilder()
      .setUpdateDraftSubjectAction(CardService.newUpdateDraftSubjectAction()
          .addUpdateSubject(subject))
      .build();
  return response;
}

/**
 * Updates the To recipients of the current email when the user clicks
 * on "Update To recipients" in the compose UI.
 *
 * Note: This is not the compose action that builds a compose UI, but
 * rather an action taken when the user interacts with the compose UI.
 *
 * @return {UpdateDraftActionResponse}
 */
function applyUpdateToRecipientsAction() {
  // Get the new To recipients of the email.
  // This function is not shown in this example.
  var toRecipients = getToRecipients();
  var response = CardService.newUpdateDraftActionResponseBuilder()
      .setUpdateDraftToRecipientsAction(CardService.newUpdateDraftToRecipientsAction()
          .addUpdateToRecipients(toRecipients))
      .build();
  return response;
}

/**
 * Updates the Cc recipients  of the current email when the user clicks
 * on "Update Cc recipients" in the compose UI.
 *
 * Note: This is not the compose action that builds a compose UI, but
 * rather an action taken when the user interacts with the compose UI.
 *
 * @return {UpdateDraftActionResponse}
 */
function applyUpdateCcRecipientsAction() {
  // Get the new Cc recipients of the email.
  // This function is not shown in this example.
  var ccRecipients = getCcRecipients();
  var response = CardService.newUpdateDraftActionResponseBuilder()
      .setUpdateDraftCcRecipientsAction(CardService.newUpdateDraftCcRecipientsAction()
          .addUpdateToRecipients(ccRecipients))
      .build();
  return response;
}

/**
 * Updates the Bcc recipients  of the current email when the user clicks
 * on "Update Bcc recipients" in the compose UI.
 *
 * Note: This is not the compose action that builds a compose UI, but
 * rather an action taken when the user interacts with the compose UI.
 *
 * @return {UpdateDraftActionResponse}
 */
function applyUpdateBccRecipientsAction() {
  // Get the new Bcc recipients of the email.
  // This function is not shown in this example.
  var bccRecipients = getBccRecipients();
  var response = CardService.newUpdateDraftActionResponseBuilder()
      .setUpdateDraftBccRecipientsAction(CardService.newUpdateDraftBccRecipientsAction()
          .addUpdateToRecipients(bccRecipients))
      .build();
  return response;
}
```

### Example 2

The following code snippet shows how to build a compose UI that inserts images into the current draft email.

```javascript
/**
 * Compose trigger function that fires when the compose UI is
 * requested. Builds and returns a compose UI for inserting images.
 *
 * @param {event} e The compose trigger event object. Not used in
 *         this example.
 * @return {Card[]}
 */
function getInsertImageComposeUI(e) {
  return [buildImageComposeCard()];
}

/**
 * Build a card to display images from a third-party source.
 *
 * @return {Card}
 */
function buildImageComposeCard() {
  // Get a short list of image URLs to display in the UI.
  // This function is not shown in this example.
  var imageUrls = getImageUrls();

  var card = CardService.newCardBuilder();
  var cardSection = CardService.newCardSection().setHeader('My Images');
  for (var i = 0; i < imageUrls.length; i++) {
    var imageUrl = imageUrls[i];
    cardSection.addWidget(
        CardService.newImage()
            .setImageUrl(imageUrl)
            .setOnClickAction(CardService.newAction()
                  .setFunctionName('applyInsertImageAction')
                  .setParameters({'url' : imageUrl})));
  }
  return card.addSection(cardSection).build();
}

/**
 * Adds an image to the current draft email when the image is clicked
 * in the compose UI. The image is inserted at the current cursor
 * location. If any content of the email draft is currently selected,
 * it is deleted and replaced with the image.
 *
 * Note: This is not the compose action that builds a compose UI, but
 * rather an action taken when the user interacts with the compose UI.
 *
 * @param {event} e The incoming event object.
 * @return {UpdateDraftActionResponse}
 */
function applyInsertImageAction(e) {
  var imageUrl = e.parameters.url;
  var imageHtmlContent = '<img style="display: block" src="'
        + imageUrl + '"/>';
  var response = CardService.newUpdateDraftActionResponseBuilder()
      .setUpdateDraftBodyAction(CardService.newUpdateDraftBodyAction()
          .addUpdateContent(
              imageHtmlContent,
              CardService.ContentType.MUTABLE_HTML)
          .setUpdateType(
              CardService.UpdateDraftBodyType.IN_PLACE_INSERT))
      .build();
  return response;
}
```
