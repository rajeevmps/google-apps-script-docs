# Build interactive dialogs

## Page Summary

- Google Chat app dialogs are interactive windows used to gather user information within the app.
- Dialogs are initiated through slash commands or button clicks and utilize cards with form inputs for user interaction.
- Upon submission, apps can display a new dialog for multi-step processes or close the dialog with an optional notification.
- Apps Script code snippets demonstrate handling dialog submissions, including validation and feedback through confirmation messages.
- Dialogs are currently part of the Google Workspace Developer Preview Program and require specific setup within Google Cloud Function or Apps Script environments.

This page describes how a Google Chat app can open dialogs
to display user interfaces (UIs) and respond to users.

**Note:** In Google Chat, add-ons appear to users as
Google Chat apps. You can also build your Chat app using 
*Google Chat API interaction events*. To learn more, see the
[Extend Google Chat overview](https://developers.google.com/workspace/add-ons/chat).

*Dialogs* are windowed, card-based interfaces
that open from a Chat space or message. The dialog and its
contents are only visible to the user who opened it.

Chat apps can use dialogs to request and collect information from
Chat users, including multi-step forms. For more details
on building form inputs, see
[Collect and process information from users](https://developers.google.com/workspace/add-ons/chat/collect-information#build-cards).

## Prerequisites

**HTTP**

A Google Workspace add-on that extends Google Chat. To build one,
complete the [HTTP
quickstart](https://developers.google.com/workspace/add-ons/chat/quickstart-http).

**Apps Script**

A Google Workspace add-on that extends Google Chat. To build one,
complete the [Apps Script quickstart](https://developers.google.com/workspace/add-ons/chat/quickstart-apps-script).

## Open a dialog

![A dialog featuring a variety of different widgets.](https://developers.google.com/static/workspace/add-ons/images/dialogs-card-1.png)

![](https://developers.google.com/static/workspace/add-ons/images/dialogs-card-1.png)

This section explains how to respond and set up a dialog by doing the following:

1. Trigger the dialog request from a user interaction.
2. Handle the request by returning and opening a dialog.
3. After users submit information, process the submission by either closing the
dialog or returning another dialog.

### Trigger a dialog request

A Chat app can only open dialogs to respond to a user
interaction, such as a command or a button click from a message in a card.

To respond to users with a dialog, a Chat app must
build an interaction that triggers the dialog request, such as the following:

- **Respond to a command.** To trigger the request from a command,
you must check the **Opens a dialog** checkbox when
[configuring the command](https://developers.google.com/workspace/add-ons/chat/commands#configure).
- **Respond to a button click** in a
[message](https://developers.google.com/workspace/chat/messages-overview),
either as part of a card or at the bottom of the message. To trigger the
request from a button in a message, you configure the
button's [`onClick`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#onclick)
action by setting its `interaction` to `OPEN_DIALOG`.

![Button that triggers a dialog](https://developers.google.com/static/workspace/add-ons/images/dialogs-open-card-click.png)

The following code sample shows how to trigger a dialog request from a button in
a card message. To open the dialog, set the field
[`onClick.action.interaction`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#google.apps.card.v1.Action.Interaction)
of the button to `OPEN_DIALOG`:

**Node.js**

```javascript
{ buttonList: { buttons: [{
  text: "ADD CONTACT",
  onClick: { action: {
    function: FUNCTION_URL,
    interaction: "OPEN_DIALOG",
    parameters: [
      { key: "actionName", value: "openInitialDialog" }
    ]
  }}
}]}}
```

**Python**

```python
{ 'buttonList': { 'buttons': [{
  'text': "ADD CONTACT",
  'onClick': { 'action': {
    'function': FUNCTION_URL,
    'interaction': "OPEN_DIALOG",
    'parameters': [
      { 'key': "actionName", 'value': "openInitialDialog" }
    ]
  }}
}]}}
```

**Java**

```java
.setButtonList(new GoogleAppsCardV1ButtonList().setButtons(List.of(new GoogleAppsCardV1Button()
  .setText("ADD CONTACT")
  .setOnClick(new GoogleAppsCardV1OnClick().setAction(new GoogleAppsCardV1Action()
    .setFunction(FUNCTION_URL)
    .setInteraction("OPEN_DIALOG")
    .setParameters(List.of(
      new GoogleAppsCardV1ActionParameter().setKey("actionName").setValue("openInitialDialog"))))))))));
```

**Apps Script**

```javascript
{ buttonList: { buttons: [{
  text: "ADD CONTACT",
  onClick: { action: {
    function: "openInitialDialog",
    interaction: "OPEN_DIALOG"
  }}
}]}}
```

### Open the initial dialog

When a user triggers a dialog request, your Chat app
receives an
[event object](https://developers.google.com/workspace/add-ons/chat/build#event-objects) with a payload
that specifies a `dialogEventType` object as `REQUEST_DIALOG`.

To open a dialog, your Chat app can respond to the
request by returning a
[`RenderActions`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#renderactions)
object with the navigation `pushCard` to display a card. The card should contain
any user interface (UI) elements, including one or more
[`sections[]`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#google.apps.card.v1.Card.FIELDS.repeated.google.apps.card.v1.Card.Section.google.apps.card.v1.Card.sections)
of widgets. To collect information from users, you can specify form input
widgets and a button widget. To learn more about designing form inputs, see
[Collect and process information from users](https://developers.google.com/workspace/add-ons/chat/collect-information#build-cards).

The following code sample shows how a Chat app returns
a response that opens a dialog:

**Node.js**

```javascript
/**
 * Opens the initial step of the dialog that lets users add contact details.
 *
 * @return {Object} open the dialog.
 */
function openInitialDialog() {
  return { action: { navigations: [{ pushCard: { sections: [{ widgets: [
    { textInput: {
      name: "contactName",
      label: "First and last name",
      type: "SINGLE_LINE"
    }},
    { dateTimePicker: {
      name: "contactBirthdate",
      label: "Birthdate",
      type: "DATE_ONLY"
    }},
    { selectionInput: {
      name: "contactType",
      label: "Contact type",
      type: "RADIO_BUTTON",
      items: [
        { text: "Work", value: "Work", selected: false },
        { text: "Personal", value: "Personal", selected: false }
      ]
    }},
    { buttonList: { buttons: [{
      text: "NEXT",
      onClick: { action: {
        function: FUNCTION_URL,
        parameters: [
          { key: "actionName", value: "openConfirmationDialog" }
        ]
      }}
    }]}}
  ]}]}}]}};
}
```

**Python**

```python
def open_initial_dialog() -> Mapping[str, Any]:
  """Opens the initial step of the dialog that lets users add contact details.

  Returns:
    Mapping[str, Any]: open the dialog.
  """
  return { 'action': { 'navigations': [{ 'pushCard': { 'sections': [{ 'widgets': [
    { 'textInput': {
      'name': "contactName",
      'label': "First and last name",
      'type': "SINGLE_LINE"
    }},
    { 'dateTimePicker': {
      'name': "contactBirthdate",
      'label': "Birthdate",
      'type': "DATE_ONLY"
    }},
    { 'selectionInput': {
      'name': "contactType",
      'label': "Contact type",
      'type': "RADIO_BUTTON",
      'items': [
        { 'text': "Work", 'value': "Work", 'selected': False },
        { 'text': "Personal", 'value': "Personal", 'selected': False }
      ]
    }},
    { 'buttonList': { 'buttons': [{
      'text': "NEXT",
      'onClick': { 'action': {
        'function': FUNCTION_URL,
        'parameters': [
          { 'key': "actionName", 'value': "openConfirmationDialog" }
        ]
      }}
    }]}}
  ]}]}}]}}
```

**Java**

```java
/**
 * Opens the initial step of the dialog that lets users add contact details.
 *
 * @return {Object} open the dialog.
 */
GenericJson openInitialDialog() {
  GoogleAppsCardV1Card cardV2 = new GoogleAppsCardV1Card()
    .setSections(List.of(new GoogleAppsCardV1Section().setWidgets(List.of(
      new GoogleAppsCardV1Widget().setTextInput(new GoogleAppsCardV1TextInput()
        .setName("contactName")
        .setLabel("First and last name")
        .setType("SINGLE_LINE")),
      new GoogleAppsCardV1Widget().setDateTimePicker(new GoogleAppsCardV1DateTimePicker()
        .setName("contactBirthdate")
        .setLabel("Birthdate")
        .setType("DATE_ONLY")),
      new GoogleAppsCardV1Widget().setSelectionInput(new GoogleAppsCardV1SelectionInput()
        .setName("contactType")
        .setLabel("Contact type")
        .setType("RADIO_BUTTON")
        .setItems(List.of(
          new GoogleAppsCardV1SelectionItem()
            .setText("Work")
            .setValue("Work")
            .setSelected(false),
          new GoogleAppsCardV1SelectionItem()
            .setText("Personal")
            .setValue("Personal")
            .setSelected(false)))),
      new GoogleAppsCardV1Widget().setButtonList(new GoogleAppsCardV1ButtonList().setButtons(List.of(
        new GoogleAppsCardV1Button()
          .setText("NEXT")
          .setOnClick(new GoogleAppsCardV1OnClick().setAction(new GoogleAppsCardV1Action()
            .setFunction(FUNCTION_URL)
            .setParameters(List.of(
              new GoogleAppsCardV1ActionParameter().setKey("actionName").setValue("openConfirmationDialog"))))))))))));
  return new GenericJson() {{
    put("action", new GenericJson() {{
      put("navigations", List.of(new GenericJson() {{
        put("pushCard", cardV2);
      }}));
    }});
  }};
}
```

**Apps Script**

```javascript
/**
 * Opens the initial step of the dialog that lets users add contact details.
 *
 * @param {Object} event The event object from the Google Workspace add-on.
 * @return {Object} open the dialog.
 */
function openInitialDialog(event) {
  return { action: { navigations: [{ pushCard: { sections: [{ widgets: [
    { textInput: {
      name: "contactName",
      label: "First and last name",
      type: "SINGLE_LINE"
    }},
    { dateTimePicker: {
      name: "contactBirthdate",
      label: "Birthdate",
      type: "DATE_ONLY"
    }},
    { selectionInput: {
      name: "contactType",
      label: "Contact type",
      type: "RADIO_BUTTON",
      items: [
        { text: "Work", value: "Work", selected: false },
        { text: "Personal", value: "Personal", selected: false }
      ]
    }},
    { buttonList: { buttons: [{
      text: "NEXT",
      onClick: { action: { function : "openConfirmationDialog" }}
    }]}}
  ]}]}}]}};
}
```

## Handle the dialog submission

When users click a button that submits a dialog, your
Chat app receives an event object with an
[`ButtonClickedPayload`](https://developers.google.com/workspace/add-ons/concepts/event-objects#buttonclickedpayload)
object. In the payload, the `dialogEventType` is set to `SUBMIT_DIALOG`. To
understand how to collect and process the information in the dialog, see
[Collect and process information from Google Chat users](https://developers.google.com/workspace/chat/read-form-data).

Your Chat app must respond to the event object by
doing one of the following:

- Return another dialog to populate another card
or form.
- Close the dialog after validating the data the user submitted, and
optionally, send a confirmation message.

### Optional: Return another dialog

After users submit the initial dialog, Chat apps can
return one or more additional dialogs to help users review information before
submitting, complete multi-step forms, or populate form content dynamically.

To process the data that users input, the Chat app
handles the data in the event's
[`commonEventObject.formInputs`](https://developers.google.com/workspace/add-ons/concepts/event-objects#common_event_object)
object. To learn more about retrieving values from input widgets, see
[Collect and process information from users](https://developers.google.com/workspace/add-ons/chat/collect-information).

To keep track of any data that users input from the initial dialog, you must add
parameters to the button that opens the next dialog. For details, see
[Transfer data to another card](https://developers.google.com/workspace/add-ons/chat/collect-information#transfer).

In this example, a Chat app opens an initial dialog
that leads to a second dialog for confirmation before submitting:

**Node.js**

```javascript
/**
 * Responds to a message in Google Chat.
 *
 * @return {Object} response that handles dialogs.
 */
function handleMessage() {
  return { hostAppDataAction: { chatDataAction: { createMessageAction: { message: {
    text: "To add a contact, use the `ADD CONTACT` button below.",
    accessoryWidgets: [
      { buttonList: { buttons: [{
        text: "ADD CONTACT",
        onClick: { action: {
          function: FUNCTION_URL,
          interaction: "OPEN_DIALOG",
          parameters: [
            { key: "actionName", value: "openInitialDialog" }
          ]
        }}
      }]}}
    ]
  }}}}};
}

/**
 * Responds to a button clicked in Google Chat.
 *
 * @param {Object} event The event object from the Google Workspace add-on.
 * @return {Object} response depending on the button clicked.
 */
function handleButtonClicked(event) {
  // Initial dialog form page
  if (event.commonEventObject.parameters.actionName === "openInitialDialog") {
    return openInitialDialog();
  // Confirmation dialog form page
  } else if (event.commonEventObject.parameters.actionName === "openConfirmationDialog") {
    return openConfirmationDialog(event);
  // Submission dialog form page
  } else if (event.commonEventObject.parameters.actionName === "submitDialog") {
    return submitDialog(event);
  }
}

/**
 * Opens the initial step of the dialog that lets users add contact details.
 *
 * @return {Object} open the dialog.
 */
function openInitialDialog() {
  return { action: { navigations: [{ pushCard: { sections: [{ widgets: [
    { textInput: {
      name: "contactName",
      label: "First and last name",
      type: "SINGLE_LINE"
    }},
    { dateTimePicker: {
      name: "contactBirthdate",
      label: "Birthdate",
      type: "DATE_ONLY"
    }},
    { selectionInput: {
      name: "contactType",
      label: "Contact type",
      type: "RADIO_BUTTON",
      items: [
        { text: "Work", value: "Work", selected: false },
        { text: "Personal", value: "Personal", selected: false }
      ]
    }},
    { buttonList: { buttons: [{
      text: "NEXT",
      onClick: { action: {
        function: FUNCTION_URL,
        parameters: [
          { key: "actionName", value: "openConfirmationDialog" }
        ]
      }}
    }]}}
  ]}]}}]}};
}

/**
 * Opens the second step of the dialog that lets users confirm details.
 *
 * @param {Object} event The event object from the Google Workspace add-on.
 * @return {Object} update the dialog.
 */
function openConfirmationDialog(event) {
  // Retrieve the form input values
  const name = event.commonEventObject.formInputs["contactName"].stringInputs.value[0];
  const birthdate = event.commonEventObject.formInputs["contactBirthdate"].dateInput.msSinceEpoch;
  const type = event.commonEventObject.formInputs["contactType"].stringInputs.value[0];
  // Display the input values for confirmation
  return { action: { navigations: [{ pushCard: { sections: [{ widgets: [
    { textParagraph: { text: "Confirm contact information and submit:" }},
    { textParagraph: { text: "<b>Name:</b> " + name }},
    { textParagraph: { text: "<b>Birthday:</b> " + new Date(birthdate) }},
    { textParagraph: { text: "<b>Type:</b> " + type }},
    { buttonList: { buttons: [{
      text: "SUBMIT",
      onClick: { action: {
        function: FUNCTION_URL,
        parameters: [
          { key: "actionName", value: "submitDialog" },
          // Pass input values as parameters for last dialog step (submission)
          { key: "contactName", value: name },
          { key: "contactBirthdate", value: birthdate },
          { key: "contactType", value: type }
        ]
      }}
    }]}}
  ]}]}}]}};
}
```

**Python**

```python
def handle_message() -> Mapping[str, Any]:
  """Responds to a message in Google Chat.

  Returns:
    Mapping[str, Any]: the response that handles dialogs.
  """
  return { 'hostAppDataAction': { 'chatDataAction': { 'createMessageAction': { 'message': {
    'text': "To add a contact, use the `ADD CONTACT` button below.",
    'accessoryWidgets': [
      { 'buttonList': { 'buttons': [{
        'text': "ADD CONTACT",
        'onClick': { 'action': {
          'function': FUNCTION_URL,
          'interaction': "OPEN_DIALOG",
          'parameters': [
            { 'key': "actionName", 'value': "openInitialDialog" }
          ]
        }}
      }]}}
    ]
  }}}}}

def handle_button_clicked(event: Mapping[str, Any]) -> Mapping[str, Any]:
  """Responds to a button clicked in Google Chat.

  Args:
    Mapping[str, Any] event: the event object from the Google Workspace add-on

  Returns:
    Mapping[str, Any]: the response depending on the button clicked.
  """
  # Initial dialog form page
  if "openInitialDialog" == event['commonEventObject']['parameters']['actionName']:
    return open_initial_dialog()
  # Confirmation dialog form page
  elif "openConfirmationDialog" == event['commonEventObject']['parameters']['actionName'] :
    return open_confirmation_dialog(event)
  # Submission dialog form page
  elif "submitDialog" == event['commonEventObject']['parameters']['actionName']:
    return submit_dialog(event)

def open_initial_dialog() -> Mapping[str, Any]:
  """Opens the initial step of the dialog that lets users add contact details.

  Returns:
    Mapping[str, Any]: open the dialog.
  """
  return { 'action': { 'navigations': [{ 'pushCard': { 'sections': [{ 'widgets': [
    { 'textInput': {
      'name': "contactName",
      'label': "First and last name",
      'type': "SINGLE_LINE"
    }},
    { 'dateTimePicker': {
      'name': "contactBirthdate",
      'label': "Birthdate",
      'type': "DATE_ONLY"
    }},
    { 'selectionInput': {
      'name': "contactType",
      'label': "Contact type",
      'type': "RADIO_BUTTON",
      'items': [
        { 'text': "Work", 'value': "Work", 'selected': False },
        { 'text': "Personal", 'value': "Personal", 'selected': False }
      ]
    }},
    { 'buttonList': { 'buttons': [{
      'text': "NEXT",
      'onClick': { 'action': {
        'function': FUNCTION_URL,
        'parameters': [
          { 'key': "actionName", 'value': "openConfirmationDialog" }
        ]
      }}
    }]}}
  ]}]}}]}}

def open_confirmation_dialog(event: Mapping[str, Any]) -> Mapping[str, Any]:
  """Opens the second step of the dialog that lets users confirm details.

  Args:
    Mapping[str, Any] event: the event object from the Google Workspace add-on

  Returns:
    Mapping[str, Any]: update the dialog.
  """
  name = event.get('commonEventObject').get('formInputs')["contactName"].get('stringInputs').get('value')[0]
  birthdateEpoch = event.get('commonEventObject').get('formInputs')["contactBirthdate"].get('dateInput').get('msSinceEpoch')
  birthdate = datetime.fromtimestamp(int(birthdateEpoch) / 1000.0).strftime("%Y-%m-%d")
  type = event.get('commonEventObject').get('formInputs')["contactType"].get('stringInputs').get('value')[0]
  # Display the input values for confirmation
  return { 'action': { 'navigations': [{ 'pushCard': { 'sections': [{ 'widgets': [
    { 'textParagraph': { 'text': "Confirm contact information and submit:" }},
    { 'textParagraph': { 'text': "<b>Name:</b> " + name }},
    { 'textParagraph': { 'text': "<b>Birthday:</b> " + birthdate }},
    { 'textParagraph': { 'text': "<b>Type:</b> " + type }},
    { 'buttonList': { 'buttons': [{
      'text': "SUBMIT",
      'onClick': { 'action': {
        'function': FUNCTION_URL,
        'parameters': [
          { 'key': "actionName", 'value': "submitDialog" },
          # Pass input values as parameters for last dialog step (submission)
          { 'key': "contactName", 'value': name },
          { 'key': "contactBirthdate", 'value': birthdate },
          { 'key': "contactType", 'value': type }
        ]
      }}
    }]}}
  ]}]}}]}}
```

**Java**

```java
/**
 * Responds to a message in Google Chat.
 *
 * @return response that handles dialogs.
 */
GenericJson handleMessage() {
  Message message = new Message()
    .setText("To add a contact, use the `ADD CONTACT` button below.")
    .setAccessoryWidgets(List.of(new AccessoryWidget()
      .setButtonList(new GoogleAppsCardV1ButtonList().setButtons(List.of(new GoogleAppsCardV1Button()
        .setText("ADD CONTACT")
        .setOnClick(new GoogleAppsCardV1OnClick().setAction(new GoogleAppsCardV1Action()
          .setFunction(FUNCTION_URL)
          .setInteraction("OPEN_DIALOG")
          .setParameters(List.of(
            new GoogleAppsCardV1ActionParameter().setKey("actionName").setValue("openInitialDialog"))))))))));
  return new GenericJson() {{
    put("hostAppDataAction", new GenericJson() {{
      put("chatDataAction", new GenericJson() {{
        put("createMessageAction", new GenericJson() {{
          put("message", message);
        }});
      }});
    }});
  }};
}

/**
 * Responds to a button clicked in Google Chat.
 *
 * @param event The event object from the Google Workspace add-on.
 * @return response depending on the button clicked.
 */
GenericJson handleButtonClicked(JsonNode event) {
  String actionName = event.at("/commonEventObject/parameters/actionName").asText();
  // Initial dialog form page
  if ("openInitialDialog".equals(actionName)) {
    return openInitialDialog();
  // Confirmation dialog form page
  } else if ("openConfirmationDialog".equals(actionName)) {
    return openConfirmationDialog(event);
  // Submission dialog form page
  } else if ("submitDialog".equals(actionName)) {
    return submitDialog(event);
  }
  return null; 
}

/**
 * Opens the initial step of the dialog that lets users add contact details.
 *
 * @return {Object} open the dialog.
 */
GenericJson openInitialDialog() {
  GoogleAppsCardV1Card cardV2 = new GoogleAppsCardV1Card()
    .setSections(List.of(new GoogleAppsCardV1Section().setWidgets(List.of(
      new GoogleAppsCardV1Widget().setTextInput(new GoogleAppsCardV1TextInput()
        .setName("contactName")
        .setLabel("First and last name")
        .setType("SINGLE_LINE")),
      new GoogleAppsCardV1Widget().setDateTimePicker(new GoogleAppsCardV1DateTimePicker()
        .setName("contactBirthdate")
        .setLabel("Birthdate")
        .setType("DATE_ONLY")),
      new GoogleAppsCardV1Widget().setSelectionInput(new GoogleAppsCardV1SelectionInput()
        .setName("contactType")
        .setLabel("Contact type")
        .setType("RADIO_BUTTON")
        .setItems(List.of(
          new GoogleAppsCardV1SelectionItem()
            .setText("Work")
            .setValue("Work")
            .setSelected(false),
          new GoogleAppsCardV1SelectionItem()
            .setText("Personal")
            .setValue("Personal")
            .setSelected(false)))),
      new GoogleAppsCardV1Widget().setButtonList(new GoogleAppsCardV1ButtonList().setButtons(List.of(
        new GoogleAppsCardV1Button()
          .setText("NEXT")
          .setOnClick(new GoogleAppsCardV1OnClick().setAction(new GoogleAppsCardV1Action()
            .setFunction(FUNCTION_URL)
            .setParameters(List.of(
              new GoogleAppsCardV1ActionParameter().setKey("actionName").setValue("openConfirmationDialog"))))))))))));
  return new GenericJson() {{
    put("action", new GenericJson() {{
      put("navigations", List.of(new GenericJson() {{
        put("pushCard", cardV2);
      }}));
    }});
  }};
}

/**
 * Opens the second step of the dialog that lets users confirm details.
 *
 * @param event The event object from the Google Workspace add-on.
 * @return update the dialog.
 */
GenericJson openConfirmationDialog(JsonNode event) {
  // Retrieve the form input values
  String name = event.at("/commonEventObject/formInputs/contactName/stringInputs/value").get(0).asText();
  String birthdateEpoch = event.at("/commonEventObject/formInputs/contactBirthdate/dateInput/msSinceEpoch").asText();
  String birthdate = new SimpleDateFormat("MM/dd/yyyy").format(new Date((long)Double.parseDouble(birthdateEpoch)));
  String type = event.at("/commonEventObject/formInputs/contactType/stringInputs/value").get(0).asText();
  // Display the input values for confirmation
  GoogleAppsCardV1Card cardV2 = new GoogleAppsCardV1Card()
    .setSections(List.of(new GoogleAppsCardV1Section().setWidgets(List.of(
      new GoogleAppsCardV1Widget().setTextParagraph(new GoogleAppsCardV1TextParagraph()
        .setText("Confirm contact information and submit:")),
      new GoogleAppsCardV1Widget().setTextParagraph(new GoogleAppsCardV1TextParagraph()
        .setText("<b>Name:</b> " + name)),
      new GoogleAppsCardV1Widget().setTextParagraph(new GoogleAppsCardV1TextParagraph()
        .setText("<b>Birthday:</b> " + birthdate)),
      new GoogleAppsCardV1Widget().setTextParagraph(new GoogleAppsCardV1TextParagraph()
        .setText("<b>Type:</b> " + type)),
      new GoogleAppsCardV1Widget().setButtonList(new GoogleAppsCardV1ButtonList().setButtons(List.of(
        new GoogleAppsCardV1Button()
          .setText("SUBMIT")
          .setOnClick(new GoogleAppsCardV1OnClick().setAction(new GoogleAppsCardV1Action()
            .setFunction(FUNCTION_URL)
            .setParameters(List.of(
              new GoogleAppsCardV1ActionParameter().setKey("actionName").setValue("submitDialog"),
              // Pass input values as parameters for last dialog step (submission)
              new GoogleAppsCardV1ActionParameter().setKey("contactName").setValue(name),
              new GoogleAppsCardV1ActionParameter().setKey("contactBirthdate").setValue(birthdate),
              new GoogleAppsCardV1ActionParameter().setKey("contactType").setValue(type))))))))))));
  return new GenericJson() {{
    put("action", new GenericJson() {{
      put("navigations", List.of(new GenericJson() {{
        put("pushCard", cardV2);
      }}));
    }});
  }};
}
```

**Apps Script**

```javascript
/**
 * Responds to a message in Google Chat.
 *
 * @param {Object} event The event object from the Google Workspace add-on.
 * @return {Object} response that handles dialogs.
 */
function onMessage(event) {
  // Reply with a message that contains a button to open the initial dialog
  return { hostAppDataAction: { chatDataAction: { createMessageAction: { message: {
    text: "To add a contact, use the `ADD CONTACT` button below.",
    accessoryWidgets: [
      { buttonList: { buttons: [{
        text: "ADD CONTACT",
        onClick: { action: {
          function: "openInitialDialog",
          interaction: "OPEN_DIALOG"
        }}
      }]}}
    ]
  }}}}};
}

/**
 * Opens the initial step of the dialog that lets users add contact details.
 *
 * @param {Object} event The event object from the Google Workspace add-on.
 * @return {Object} open the dialog.
 */
function openInitialDialog(event) {
  return { action: { navigations: [{ pushCard: { sections: [{ widgets: [
    { textInput: {
      name: "contactName",
      label: "First and last name",
      type: "SINGLE_LINE"
    }},
    { dateTimePicker: {
      name: "contactBirthdate",
      label: "Birthdate",
      type: "DATE_ONLY"
    }},
    { selectionInput: {
      name: "contactType",
      label: "Contact type",
      type: "RADIO_BUTTON",
      items: [
        { text: "Work", value: "Work", selected: false },
        { text: "Personal", value: "Personal", selected: false }
      ]
    }},
    { buttonList: { buttons: [{
      text: "NEXT",
      onClick: { action: { function : "openConfirmationDialog" }}
    }]}}
  ]}]}}]}};
}

/**
 * Opens the second step of the dialog that lets users confirm details.
 *
 * @param {Object} event The event object from the Google Workspace add-on.
 * @return {Object} update the dialog.
 */
function openConfirmationDialog(event) {
  // Retrieve the form input values
  const name = event.commonEventObject.formInputs["contactName"].stringInputs.value[0];
  const birthdate = event.commonEventObject.formInputs["contactBirthdate"].dateInput.msSinceEpoch;
  const type = event.commonEventObject.formInputs["contactType"].stringInputs.value[0];
  // Display the input values for confirmation
  return { action: { navigations: [{ pushCard: { sections: [{ widgets: [
    { textParagraph: { text: "Confirm contact information and submit:" }},
    { textParagraph: { text: "<b>Name:</b> " + name }},
    { textParagraph: { text: "<b>Birthday:</b> " + new Date(birthdate) }},
    { textParagraph: { text: "<b>Type:</b> " + type }},
    { buttonList: { buttons: [{
      text: "SUBMIT",
      onClick: { action: {
        function: "submitDialog",
        // Pass input values as parameters for last dialog step (submission)
        parameters: [
          { key: "contactName", value: name },
          { key: "contactBirthdate", value: birthdate },
          { key: "contactType", value: type }
        ]
      }}
    }]}}
  ]}]}}]}};
}
```

### Close the dialog

When users click a submit button on a dialog, your
Chat app executes its associated action and provides
the event object with `buttonClickedPayload` set to the following:

- `isDialogEvent` is `true`.
- `dialogEventType` is `SUBMIT_DIALOG`.

The Chat app should return a
[`RenderActions`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#renderactions)
object with
[`EndNavigation`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#endnavigation)
set to `CLOSE_DIALOG`.

#### Optional: Display a temporary notification

When you close the dialog, you can also display a temporary text notification
to the user who is interacting with the app.

To display a notification, return the
[`RenderActions`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#renderactions)
object with the field `notification` set.

The following example closes the dialog with a text notification:

**Node.js**

```javascript
// Validate the parameters.
if (!event.commonEventObject.parameters["contactName"]) {
  return { action: {
    navigations: [{ endNavigation: { action: "CLOSE_DIALOG"}}],
    notification: { text: "Failure, the contact name was missing!" }
  }};
}
```

**Python**

```python
# Validate the parameters.
if event.get('commonEventObject').get('parameters')["contactName"] == "":
  return { 'action': {
    'navigations': [{ 'endNavigation': { 'action': "CLOSE_DIALOG"}}],
    'notification': { 'text': "Failure, the contact name was missing!" }
  }}
```

**Java**

```java
    // Validate the parameters.
    if (event.at("/commonEventObject/parameters/contactName").asText().isEmpty()) {
      return new GenericJson() {{
        put("action", new GenericJson() {{
          put("navigations", List.of(new GenericJson() {{
            put("endNavigation", new GenericJson() {{
              put("action", "CLOSE_DIALOG");
            }});
          }}));
          put("notification", new GenericJson() {{
            put("text", "Failure, the contact name was missing!");
          }});
        }});
      }};
    }

    return new GenericJson() {{
      put("hostAppDataAction", new GenericJson() {{
        put("chatDataAction", new GenericJson() {{
          put("createMessageAction", new GenericJson() {{
            put("message", new Message()
              .setText( "✅ " + event.at("/commonEventObject/parameters/contactName").asText() +
                        " has been added to your contacts."));
          }});
        }});
      }});
    }};
  }
}
```

**Apps Script**

```javascript
// Validate the parameters.
if (!event.commonEventObject.parameters["contactName"]) {
  return { action: {
    navigations: [{ endNavigation: { action: "CLOSE_DIALOG"}}],
    notification: { text: "Failure, the contact name was missing!" }
  }};
}
```

For details about passing parameters between dialogs, see
[Transfer data to another card](https://developers.google.com/workspace/add-ons/chat/collect-information#transfer).

#### Optional: Send a confirmation Chat message

When you close the dialog, you can also send a new Chat message,
or update an existing one.

To send a new message, return a
[`DataActions`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#google.apps.card.v1.DataActions)
object with the field
`CreateMessageAction` set with the new message. For example, to close the dialog
and send a text message, return the following:

The following example closes the dialog by sending a new message:

**Node.js**

```javascript
return { hostAppDataAction: { chatDataAction: { createMessageAction: { message: {
  text: "✅ " + event.commonEventObject.parameters["contactName"] + " has been added to your contacts."
}}}}};
```

**Python**

```python
return { 'hostAppDataAction': { 'chatDataAction': { 'createMessageAction': { 'message': {
  'text': "✅ " + event.get('commonEventObject').get('parameters')["contactName"] + " has been added to your contacts."
}}}}}
```

**Java**

```java
return new GenericJson() {{
  put("hostAppDataAction", new GenericJson() {{
    put("chatDataAction", new GenericJson() {{
      put("createMessageAction", new GenericJson() {{
        put("message", new Message()
          .setText( "✅ " + event.at("/commonEventObject/parameters/contactName").asText() +
                    " has been added to your contacts."));
      }});
    }});
  }});
}};
```

**Apps Script**

```javascript
return { hostAppDataAction: { chatDataAction: { createMessageAction: { message: {
  text: "✅ " + event.commonEventObject.parameters["contactName"] + " has been added to your contacts."
}}}}};
```

To update a message after the user submits a dialog, return a `DataActions`
object that contains one of the following actions:

- [`UpdateMessageAction`](https://developers.google.com/workspace/add-ons/reference/rpc/apps.extensions.markup#updatemessageaction):
[Updates a message](https://developers.google.com/workspace/add-ons/chat/send-messages#update-message)
sent by the Chat app, such as the message from
which the user requested the dialog.
- [`UpdateInlinePreviewAction`](https://developers.google.com/workspace/add-ons/reference/rpc/apps.extensions.markup#updateinlinepreviewaction):
Updates the card from a
[link preview](https://developers.google.com/workspace/add-ons/chat/preview-links).

## Troubleshoot

When a Google Chat app or
 [card](https://developers.google.com/workspace/chat/create-messages#create) returns an error, the
 Chat interface surfaces a message saying "Something went wrong."
 or "Unable to process your request." Sometimes the Chat UI
 doesn't display any error message, but the Chat app or
 card produces an unexpected result; for example, a card message might not
 appear.

Although an error message might not display in the Chat UI,
 descriptive error messages and log data are available to help you fix errors
 when error logging for Chat apps is turned on. For help viewing,
 debugging, and fixing errors, see
 [Troubleshoot and fix Google Chat errors](https://developers.google.com/workspace/chat/troubleshoot).
