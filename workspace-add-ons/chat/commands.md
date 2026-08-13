# Respond to Google Chat app commands

## Overview

This page explains how to set up and respond to commands as a Google Chat app.

**Note:** In Google Chat, add-ons appear to users as Google Chat apps. You can also build your Chat app using *Google Chat API interaction events*. To learn more, see the [Extend Google Chat overview](/workspace/add-ons/chat).

Commands help users discover and use key features of a Chat app. Only Chat apps can see the content of a command. For example, if a user sends a message with a slash command, the message is only visible to the user and the Chat app.

To decide whether you should build commands, and to understand how to design user interactions, see [Define all user journeys](/workspace/chat/journeys).

## Types of Chat app commands

You can build Chat app commands as slash commands, quick commands, or message actions. To use each type of command, users can do the following:

1. **Slash commands:** Users can select a slash command from the menu or type a slash (`/`) and then a predefined text, such as `/about`. Chat apps typically require argument text for the slash command.

   Create a slash command if your Chat app requires additional input from the user. For example, you can create a slash command called `/search` that runs after the user enters a phrase to search for, like `/search receipts`.

2. **Quick commands:** Users use commands by opening the menu from the reply area of a Chat message. To use a command, they click **Add** and select a command from the menu.

   Create a quick command if your Chat app can respond to the user immediately, without waiting for additional input. For example, you can create a quick command called **Random image** that responds immediately with an image.

3. **Message actions:** (Developer Preview) Users use message actions by hovering over a message and clicking on the three-dot menu. To use a command, they open the three-dot menu and select a command from the menu.

   Create a message action if your Chat app can perform actions based on the context of a message.

## Prerequisites

### HTTP

A Google Workspace add-on that extends Google Chat. To build one, complete the [HTTP quickstart](/workspace/add-ons/chat/quickstart-http).

**Note:** The code samples in this guide are written to run as a [Google Cloud Run function](https://cloud.google.com/functions/docs/quickstarts) for Node.js.

### Apps Script

A Google Workspace add-on that extends Google Chat. To build one, complete the [Apps Script quickstart](/workspace/add-ons/chat/quickstart-apps-script).

## Set up the command

This section explains how to complete the following steps to set up a command:

1. Create a name and description for the command.
2. Configure the command in the Google Cloud console.

### Name and describe the command

The name of a command is what users type or select to invoke the Chat app. A short description also appears below the name, to prompt users further about how to use the command.

When choosing a name and description for your command, consider the following recommendations:

#### To name a command:

* Use short, descriptive, and actionable words or phrases to make the commands clear to the user. For example, instead of the name `Create a reminder`, use `Remind me`.
* Consider using a unique or common name for your command. If your command describes a typical interaction or feature, you can use a common name that users recognize and expect, such as `Settings` or `Feedback`. Otherwise, try to use unique command names, because if your command name is the same for other Chat apps, the user must filter through similar commands to find and use yours.

#### To describe a command:

* Keep the description short and clear so that users know what to expect when they use the command.
* Let users know if there are any formatting requirements for the command. For example, if you create a slash command that requires argument text, set the description to something like `Remind me to do [something] at [time]`.
* Let users know if the Chat app replies to everyone in the space, or privately to the user who invokes the command. For example, for the quick command `About`, you could describe it as `Learn about this app (Only visible to you)`.

### Configure the command in the Google Cloud console

To create a slash command, quick command, or message action, you specify information about the command or action in your Chat app's configuration for the Google Chat API.

To configure a command in the Google Chat API, complete the following steps:

1. In the Google Cloud console, click Menu menu > **APIs & Services** > **Enabled APIs & Services** > **Google Chat API**

2. Click **Configuration**.

3. Under **Connection settings**, go to **Triggers** and specify your endpoint details. You must use this trigger in the following section to respond to the command.

   1. **HTTP endpoint URL**: You may specify one common HTTP endpoint URL here. Alternatively, to use different HTTP endpoints for different triggers, specify the endpoint directly in the **App command** field.
   2. **Apps Script**: Enter the Apps Script Deployment ID. By default, the `onAppCommand` function will be invoked. To use a different Apps Script function, specify the custom function name in the **App command** field.

4. Under **Commands**, click **Add a command**.

5. Enter the following information about the command:

   1. **Command ID:** a number from 1 to 1000 that your Chat app uses to recognize the command and return a response.
   2. **Description:** the text that describes how to use and format the command. Descriptions can be up to 50 characters.
   3. **Command type:** select either **Quick command**, **Slash command**, or **Message action**.
   4. Specify a name for the command:
      * **Quick command name:** The display name that users select from the menu to invoke the command. Can be up to 50 characters and include special characters. For example, `Remind me`.
      * **Slash command name:** The text that users type to invoke the command in a message. Must start with a slash, contain only text, and can be up to 50 characters. For example, `/remindMe`.
      * **Message action name:** (Developer Preview) The display name that users select from the menu to invoke the message action. Can be up to 50 characters and include special characters. For example, `Remind me`.

6. Optional: **Loading notification message**: (Developer Preview) A toast notification message to display to the user while the message action is executing. Only available for message actions that don't open dialogs.

7. Optional: If you want your Chat app to respond to the command with a dialog, select the **Open a dialog** checkbox.

8. Click **Save**.

The command is now configured for the Chat app.

## Respond to a command

When users use a command, your Chat app receives an [event object](/workspace/add-ons/chat/build#event-objects). The event payload contains an [`appCommandPayload`](/workspace/add-ons/concepts/event-objects#appcommandpayload) object with details about the command that was invoked (including the command ID and the command type), so that you can return an appropriate response. The event object is sent to the HTTP endpoint or Apps Script function that you specified when you configured the **App command** trigger.

The following code shows an example of a Chat app that replies to the slash command `/about` with a text message. To respond to slash commands, the Chat app handles event objects from an **App command** trigger. When the payload of an event object contains a slash command ID, Chat app returns the action `DataActions` with a [`createMessageAction`](/workspace/add-ons/reference/rpc/apps.extensions.markup#apps.extensions.markup.ChatDataActionMarkup.CreateMessageAction) object:

### Node.js

```javascript
// The ID of the slash command "/about".
// You must use the same ID in the Google Chat API configuration.
const ABOUT_COMMAND_ID = 1;

/**
 * Handle requests from Google Workspace add on
 *
 * @param {Object} req Request sent by Google Chat
 * @param {Object} res Response to be sent back to Google Chat
 */
http('avatarApp', (req, res) => {
  const chatEvent = req.body.chat;
  let message;
  if (chatEvent.appCommandPayload) {
    message = handleAppCommand(chatEvent);
  } else {
    message = handleMessage(chatEvent);
  }
  res.send({ hostAppDataAction: { chatDataAction: { createMessageAction: {
    message: message
  }}}});
});

/**
 * Responds to an APP_COMMAND event in Google Chat.
 *
 * @param {Object} event the event object from Google Chat
 * @return the response message object.
 */
function handleAppCommand(event) {
  switch (event.appCommandPayload.appCommandMetadata.appCommandId) {
    case ABOUT_COMMAND_ID:
      return {
        text: 'The Avatar app replies to Google Chat messages.'
      };
  }
}
```

### Python

```python
# The ID of the slash command "/about".
# You must use the same ID in the Google Chat API configuration.
ABOUT_COMMAND_ID = 1

@functions_framework.http
def avatar_app(req: flask.Request) -> Mapping[str, Any]:
  """Handle requests from Google Workspace add on

  Args:
    flask.Request req: the request sent by Google Chat

  Returns:
    Mapping[str, Any]: the response to be sent back to Google Chat
  """
  chat_event = req.get_json(silent=True)["chat"]
  if chat_event and "appCommandPayload" in chat_event:
    message = handle_app_command(chat_event)
  else:
    message = handle_message(chat_event)
  return { "hostAppDataAction": { "chatDataAction": { "createMessageAction": {
      "message": message
  }}}}

def handle_app_command(event: Mapping[str, Any]) -> Mapping[str, Any]:
  """Responds to an APP_COMMAND event in Google Chat.

  Args:
    Mapping[str, Any] event: the event object from Google Chat

  Returns:
    Mapping[str, Any]: the response message object.
  """
  if event["appCommandPayload"]["appCommandMetadata"]["appCommandId"] == ABOUT_COMMAND_ID:
    return {
      "text": "The Avatar app replies to Google Chat messages.",
    }
  return {}
```

### Java

```java
// The ID of the slash command "/about".
// You must use the same ID in the Google Chat API configuration.
private static final int ABOUT_COMMAND_ID = 1;

private static final Gson gson = new Gson();

/**
 * Handle requests from Google Workspace add on
 * 
 * @param request the request sent by Google Chat
 * @param response the response to be sent back to Google Chat
 */
@Override
public void service(HttpRequest request, HttpResponse response) throws Exception {
  JsonObject event = gson.fromJson(request.getReader(), JsonObject.class);
  JsonObject chatEvent = event.getAsJsonObject("chat");
  Message message;
  if (chatEvent.has("appCommandPayload")) {
    message = handleAppCommand(chatEvent);
  } else {
    message = handleMessage(chatEvent);
  }
  JsonObject createMessageAction = new JsonObject();
  createMessageAction.add("message", gson.fromJson(gson.toJson(message), JsonObject.class));
  JsonObject chatDataAction = new JsonObject();
  chatDataAction.add("createMessageAction", createMessageAction);
  JsonObject hostAppDataAction = new JsonObject();
  hostAppDataAction.add("chatDataAction", chatDataAction);
  JsonObject dataActions = new JsonObject();
  dataActions.add("hostAppDataAction", hostAppDataAction);
  response.getWriter().write(gson.toJson(dataActions));
}

/**
 * Handles an APP_COMMAND event in Google Chat.
 *
 * @param event the event object from Google Chat
 * @return the response message object.
 */
private Message handleAppCommand(JsonObject event) throws Exception {
  switch (event.getAsJsonObject("appCommandPayload")
    .getAsJsonObject("appCommandMetadata").get("appCommandId").getAsInt()) {
    case ABOUT_COMMAND_ID:
      return new Message()
        .setText("The Avatar app replies to Google Chat messages.");
    default:
      return null;
  }
}
```

### Apps Script

```javascript
// The ID of the slash command "/about".
// You must use the same ID in the Google Chat API configuration.
const ABOUT_COMMAND_ID = 1;

/**
 * Responds to an APP_COMMAND event in Google Chat.
 *
 * @param {Object} event the event object from Google Chat
 */
function onAppCommand(event) {
  // Executes the app command logic based on ID.
  switch (event.chat.appCommandPayload.appCommandMetadata.appCommandId) {
    case ABOUT_COMMAND_ID:
      return { hostAppDataAction: { chatDataAction: { createMessageAction: { message: {
        text: 'The Avatar app replies to Google Chat messages.'
      }}}}};
  }
}
```

To use this code sample, replace `ABOUT_COMMAND_ID` with the command ID that you specified when you configured the command in the Chat API.

### Respond to a message action

**Developer Preview:** Available as part of the [Google Workspace Developer Preview Program](https://developers.google.com/workspace/preview), which grants early access to certain features.

The following code shows an example of a Chat app that replies to the message action **Remind me** with a text message. To respond to message actions, the Chat app handles event objects from an **App command** trigger. When the payload of an event object contains a message action command ID, Chat app returns the action `DataActions` with a [`createMessageAction`](/workspace/add-ons/reference/rpc/apps.extensions.markup#apps.extensions.markup.ChatDataActionMarkup.CreateMessageAction) object:

#### Node.js

```javascript
/**
 * Responds to an APP_COMMAND interaction event from Google Chat.
 *
 * @param {Object} event The interaction event from Google Chat.
 * @param {Object} res The HTTP response object.
 * @return {Object} The JSON response message with a confirmation.
 */
function onAppCommand(event, res) {
  // Collect the command ID and type from the event metadata.
  const {appCommandId, appCommandType} =
    event.chat.appCommandPayload.appCommandMetadata;

  if (appCommandType === 'MESSAGE_ACTION' &&
      appCommandId === REMIND_ME_COMMAND_ID) {

    // Message actions can access the context of the message they were
    // invoked on, such as the text or sender of that message.
    const messageText = event.chat.appCommandPayload.message.text;

    // Return a response that includes details from the original message.
    return res.json({
      "hostAppDataAction": {
        "chatDataAction": {
          "createMessageAction": {
            "message": {
              "text": `Setting a reminder for message: "${messageText}"`
            }
          }
        }
      }
    });
  }
}
```

#### Python

```python
def on_app_command(event):
    """Responds to an APP_COMMAND interaction event from Google Chat.

    Args:
        event (dict): The interaction event from Google Chat.

    Returns:
        dict: The JSON response message with a confirmation.
    """
    # Collect the command ID and type from the event metadata.
    payload = event.get('chat', {}).get('appCommandPayload', {})
    metadata = payload.get('appCommandMetadata', {})
    if metadata.get('appCommandType') == 'MESSAGE_ACTION' and \
       metadata.get('appCommandId') == REMIND_ME_COMMAND_ID:

        # Message actions can access the context of the message they were
        # invoked on, such as the text or sender of that message.
        message_text = payload.get('message', {}).get('text')

        # Return a response that includes details from the original message.
        return {
            "hostAppDataAction": {
                "chatDataAction": {
                    "createMessageAction": {
                        "message": {
                            "text": f'Setting a reminder for message: "{message_text}"'
                        }
                    }
                }
            }
        }
```

#### Java

```java
/**
 * Responds to an APP_COMMAND interaction event from Google Chat.
 *
 * @param event The interaction event from Google Chat.
 * @param response The HTTP response object.
 */
void onAppCommand(JsonObject event, HttpResponse response) throws Exception {
  // Collect the command ID and type from the event metadata.
  JsonObject payload = event.getAsJsonObject("chat").getAsJsonObject("appCommandPayload");
  JsonObject metadata = payload.getAsJsonObject("appCommandMetadata");
  String appCommandType = metadata.get("appCommandType").getAsString();

  if (appCommandType.equals("MESSAGE_ACTION")) {
    int commandId = metadata.get("appCommandId").getAsInt();
    if (commandId == REMIND_ME_COMMAND_ID) {
      // Message actions can access the context of the message they were
      // invoked on, such as the text or sender of that message.
      String messageText = payload.getAsJsonObject("message").get("text").getAsString();

      // Return a response that includes details from the original message.
      JsonObject responseMessage = new JsonObject();
      responseMessage.addProperty("text", "Setting a reminder for message: " + messageText);

      JsonObject createMessageAction = new JsonObject();
      createMessageAction.add("message", responseMessage);

      JsonObject chatDataAction = new JsonObject();
      chatDataAction.add("createMessageAction", createMessageAction);

      JsonObject hostAppDataAction = new JsonObject();
      hostAppDataAction.add("chatDataAction", chatDataAction);

      JsonObject finalResponse = new JsonObject();
      finalResponse.add("hostAppDataAction", hostAppDataAction);

      response.getWriter().write(finalResponse.toString());
    }
  }
}
```

#### Apps Script

```javascript
/**
 * Responds to an APP_COMMAND interaction event in Google Chat.
 *
 * @param {Object} event The interaction event from Google Chat.
 * @return {Object} The JSON response message with a confirmation.
 */
function onAppCommand(event) {
  // Collect the command ID and type from the event metadata.
  const {appCommandId, appCommandType} =
    event.chat.appCommandPayload.appCommandMetadata;

  if (appCommandType === 'MESSAGE_ACTION' &&
      appCommandId === REMIND_ME_COMMAND_ID) {

    // Message actions can access the context of the message they were
    // invoked on, such as the text or sender of that message.
    const messageText = event.chat.appCommandPayload.message.text;

    // Return a response that includes details from the original message.
    return CardService.newChatResponseBuilder()
        .setText("Setting a reminder for message: " + messageText)
        .build();
  }
}
```

To use this code sample, replace `REMIND_ME_COMMAND_ID` with the command ID that you specified when you configured the command in the Chat API.

## Test the command

To test the command and code, see [Test interactive features for Google Chat apps](/workspace/chat/test-interactive-features).

To learn how to test and use the command in the Chat UI, see [Use apps in Google Chat](https://support.google.com/chat/answer/7655820) in the Google Chat Help documentation.

## Related topics

* [View Chat app samples](/workspace/chat/samples) that use commands
* [Send a message](/workspace/chat/create-messages)
* [Open interactive dialogs](/workspace/chat/dialogs)
