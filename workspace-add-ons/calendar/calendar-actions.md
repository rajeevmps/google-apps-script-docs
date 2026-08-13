# Calendar actions

Action objects let you build interactive behavior into Google Workspace add-ons. They define what happens when a user interacts with a widget (for example, a button) in the add-on UI.

An action is attached to a given widget using a widget handler function, which also defines the condition that triggers the action. When triggered, the action executes a designated callback function. The callback function is passed an event object that carries information about the user's client-side interactions. You must implement the callback function and have it return a specific response object.

For example, say you want a button that builds and displays a new card when clicked. For this, you must create a new button widget and use the button widget handler function `setOnClickAction(action)` to set a card-building Action. The Action you define specifies an Apps Script callback function that executes when the button is clicked. In this case, you implement the callback function to build the card you want and return an `ActionResponse` object. The response object tells the add-on to display the card the callback function built.

This page describes Calendar-specific widget actions you can include in your add-on.

## Google Calendar interactions

Google Workspace add-ons that extend Calendar can include additional Calendar-specific widget actions. These actions require the associated action callback function to return specialized response objects:

| Action attempted | Callback function should return |
|---|---|
| Adding attendees | `CalendarEventActionResponse` |
| Setting conference data | `CalendarEventActionResponse` |
| Adding attachments | `CalendarEventActionResponse` |

To use these widget actions and response objects, all the following must be true:

- The action is triggered while the user has a Calendar event open.
- The Google Workspace add-on's `addOns.calendar.currentEventAccess` manifest field is set to `WRITE` or `READ_WRITE`.
- The add-on includes the `https://www.googleapis.com/auth/calendar.addons.current.event.write` Calendar scope.

Changes made by the action callback function aren't saved until the user saves the Calendar event.

## Add attendees with a callback function

The following example shows how to create a button that adds a specific attendee to a Calendar event being edited. This example uses a basic card structure:

```javascript
/**
 * Build a basic card with a button that sends a notification.
 * This function is called as part of the eventOpenTrigger that builds
 * a UI when the user opens an event.
 *
 * @param e The event object passed to eventOpenTrigger function.
 * @return {Card}
 */
function buildSimpleCard(e) {
  var buttonAction = CardService.newAction()
      .setFunctionName('onAddAttendeesButtonClicked');
  var button = CardService.newTextButton()
      .setText('Add new attendee')
      .setOnClickAction(buttonAction);

  // Check the event object to determine if the user can add
  // attendees and disable the button if not.
  if (!e.calendar.capabilities.canAddAttendees) {
    button.setDisabled(true);
  }

  // ...continue creating card sections and widgets, then create a Card
  // object to add them to. Return the built Card object.
}

/**
 * Callback function for a button action. Adds attendees to the
 * Calendar event being edited.
 *
 * @param {Object} e The action event object.
 * @return {CalendarEventActionResponse}
 */
function onAddAttendeesButtonClicked (e) {
  return CardService.newCalendarEventActionResponseBuilder()
      .addAttendees(["aiko@example.com", "malcom@example.com"])
      .build();
}
```

## Set conference data with a callback function

This action sets the conference data on the open event. For this conference data the conference solution ID needs to be specified, because the action was not triggered by the user selecting the desired solution.

The following example shows how to create a button that sets conference data for an event being edited:

```javascript
/**
 * Build a basic card with a button that sends a notification.
 * This function is called as part of the eventOpenTrigger that builds
 * a UI when the user opens a Calendar event.
 *
 * @param e The event object passed to eventOpenTrigger function.
 * @return {Card}
 */
function buildSimpleCard(e) {
  var buttonAction = CardService.newAction()
      .setFunctionName('onSaveConferenceOptionsButtonClicked')
      .setParameters(
          {'phone': "1555123467", 'adminEmail': "joyce@example.com"});
  var button = CardService.newTextButton()
      .setText('Add new attendee')
      .setOnClickAction(buttonAction);

  // Check the event object to determine if the user can set
  // conference data and disable the button if not.
  if (!e.calendar.capabilities.canSetConferenceData) {
    button.setDisabled(true);
  }

  // ...continue creating card sections and widgets, then create a Card
  // object to add them to. Return the built Card object.
}

/**
 * Callback function for a button action. Sets conference data for the
 * Calendar event being edited.
 *
 * @param {Object} e The action event object.
 * @return {CalendarEventActionResponse}
 */
function onSaveConferenceOptionsButtonClicked(e) {
  var parameters = e.commonEventObject.parameters;

  // Create an entry point and a conference parameter.
  var phoneEntryPoint = ConferenceDataService.newEntryPoint()
      .setEntryPointType(ConferenceDataService.EntryPointType.PHONE)
      .setUri('tel:' + parameters['phone']);

  var adminEmailParameter = ConferenceDataService.newConferenceParameter()
      .setKey('adminEmail')
      .setValue(parameters['adminEmail']);

  // Create a conference data object to set to this Calendar event.
  var conferenceData = ConferenceDataService.newConferenceDataBuilder()
      .addEntryPoint(phoneEntryPoint)
      .addConferenceParameter(adminEmailParameter)
      .setConferenceSolutionId('myWebScheduledMeeting')
      .build();

  return CardService.newCalendarEventActionResponseBuilder()
      .setConferenceData(conferenceData)
      .build();
}
```

## Add attachments with a callback function

The following example shows how to create a button that adds an attachment to a Calendar event being edited:

```javascript
/**
 * Build a basic card with a button that creates a new attachment.
 * This function is called as part of the eventAttachmentTrigger that
 * builds a UI when the user goes through the add-attachments flow.
 *
 * @param e The event object passed to eventAttachmentTrigger function.
 * @return {Card}
 */
function buildSimpleCard(e) {
  var buttonAction = CardService.newAction()
      .setFunctionName('onAddAttachmentButtonClicked');
  var button = CardService.newTextButton()
      .setText('Add a custom attachment')
      .setOnClickAction(buttonAction);

  // Check the event object to determine if the user can add
  // attachments and disable the button if not.
  if (!e.calendar.capabilities.canAddAttachments) {
    button.setDisabled(true);
  }

  // ...continue creating card sections and widgets, then create a Card
  // object to add them to. Return the built Card object.
}

/**
 * Callback function for a button action. Adds attachments to the
 * Calendar event being edited.
 *
 * @param {Object} e The action event object.
 * @return {CalendarEventActionResponse}
 */
function onAddAttachmentButtonClicked(e) {
  return CardService.newCalendarEventActionResponseBuilder()
      .addAttachments([
        CardService.newAttachment()
            .setResourceUrl("https://example.com/test")
            .setTitle("Custom attachment")
            .setMimeType("text/html")
            .setIconUrl("https://example.com/test.png")
      ])
      .build();
}
```

## Set the attachment icon

The attachment icon must be hosted on Google's infrastructure. See Provide attachment icons for details.
