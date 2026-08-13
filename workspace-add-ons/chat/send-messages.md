# Send Google Chat messages

## Page Summary

- This guide explains how Google Chat apps can send and update messages in response to user interactions like slash commands, button clicks, or added to space triggers.
- Google Chat apps can include text, cards, and widgets in their messages and can reply using actions or the Google Chat API.
- You should use the Google Chat API for tasks such as scheduled messages, responses exceeding 30 seconds, and messaging outside the interaction space.
- To build a Google Chat app, you'll need Node.js or Apps Script and a Google Workspace add-on extending Google Chat.
- This feature is available as part of the Google Workspace Developer Preview Program for early access.

This page explains how Google Chat apps can send messages to reply to user
interactions.

**Note:** In Google Chat, add-ons appear to users as
Google Chat apps. You can also build your Chat app using 
*Google Chat API interaction events*. To learn more, see the
[Extend Google Chat overview](https://developers.google.com/workspace/add-ons/chat).

- A
 Chat app responds to a slash command with a text message and button.
- A
 Chat app opens a dialog where users can input information.
- A
 Chat app sends a message with text and an interactive card.

## Prerequisites

**HTTP**

A Google Workspace add-on that extends Google Chat. To build one,
complete the
[HTTP quickstart](https://developers.google.com/workspace/add-ons/chat/quickstart-http).

**Apps Script**

A Google Workspace add-on that extends Google Chat. To build one,
complete the
[Apps Script quickstart](https://developers.google.com/workspace/add-ons/chat/quickstart-apps-script).

## Design the message

Chat apps can include any of the following in a message:

- Text that contains hyperlinks, @mentions, and emoji.
- One or more cards, which can appear in a message or open in a
new window as a dialog.
- One or more accessory widgets, which are buttons that appear after any text
or cards in a message.

To learn about designing messages, see the following
Google Chat API documentation:

- [Messaging overview](https://developers.google.com/workspace/chat/messages-overview)
- [Format messages](https://developers.google.com/workspace/chat/format-messages)
- [Build cards for Google Chat apps](https://developers.google.com/workspace/chat/design-components-card-dialog)
- [Add text and images to cards](https://developers.google.com/workspace/chat/add-text-image-card-dialog)
- [Add interactive UI elements to cards](https://developers.google.com/workspace/chat/design-interactive-card-dialog)

## Reply with a message

Chat apps can respond with a message to any of the following
triggers or interactions:

- [**Message** triggers](https://developers.google.com/workspace/add-ons/chat/build#TRIGGER.MESSAGE), such as
when users @mention or direct message a Chat app.
- [**Added to space** triggers](https://developers.google.com/workspace/add-ons/chat/build#TRIGGER.ADDED_TO_SPACE),
such as when users install the Chat app from the
Google Workspace Marketplace or add it to a space.
- Button clicks from cards in messages or dialogs. For example, when users
input information and click submit.

Otherwise, Chat apps can send messages proactively by
calling the Google Chat API.

To reply with a message, return the action `DataActions` with a
[`CreateMessageAction`](https://developers.google.com/workspace/add-ons/reference/rpc/apps.extensions.markup#apps.extensions.markup.ChatDataActionMarkup.CreateMessageAction) object:

```json
{ "hostAppDataAction": { "chatDataAction": { "createMessageAction": {
  "message": MESSAGE
}}}
```

Replace `MESSAGE` with a
[`Message`](https://developers.google.com/workspace/chat/api/reference/rest/v1/spaces.messages)
resource from the Chat API. To learn more about how actions work, see
[Chat actions](https://developers.google.com/workspace/add-ons/chat/build#actions).

In the following example, a Chat app creates and sends
a text message whenever it's added to a space. To send a text message when a
user adds your Chat app
to a space, your Chat app responds to the
**Added to space** trigger by returning the action `DataActions`:

**Node.js**

```javascript
/**
 * Sends an onboarding message when the Chat app is added to a space.
 *
 * @param {Object} req The request object from Google Workspace add-on.
 * @param {Object} res The response object from the Chat app.
 */
exports.cymbalApp = function cymbalApp(req, res) {
  const chatEvent = req.body.chat;
  // Send an onboarding message when added to a Chat space
  if (chatEvent.addedToSpacePayload) {
    res.json({ hostAppDataAction: { chatDataAction: { createMessageAction: { message: {
      text: 'Hi, Cymbal at your service. I help you manage your calendar' +
        'from Google Chat. Take a look at your schedule today by typing' +
        '`/checkCalendar`, or schedule a meeting with `/scheduleMeeting`. ' +
        'To learn what else I can do, type `/help`.'
    }}}}});
  }
};
```

**Python**

```python
from flask import Flask, request, json
app = Flask(__name__)

@app.route('/', methods=['POST'])
def cymbal_app():
  """Sends an onboarding message when the Chat app is added to a space.

  Returns:
    Mapping[str, Any]: The response object from the Chat app.
  """
  chat_event = request.get_json()["chat"]
  if "addedToSpacePayload" in chat_event:
    return json.jsonify({ "hostAppDataAction": { "chatDataAction": {
      "createMessageAction": { "message": {
        "text": 'Hi, Cymbal at your service. I help you manage your calendar' +
        'from Google Chat. Take a look at your schedule today by typing' +
        '`/checkCalendar`, or schedule a meeting with `/scheduleMeeting`. ' +
        'To learn what else I can do, type `/help`.'
      }}
    }}})
```

**Java**

```java
@SpringBootApplication
@RestController
public class App {
  public static void main(String[] args) {
    SpringApplication.run(App.class, args);
  }

  /*
   * Sends an onboarding message when the Chat app is added to a space.
   *
   * @return The response object from the Chat app.
   */
  @PostMapping("/")
  @ResponseBody
  public GenericJson onEvent(@RequestBody JsonNode event) throws Exception {
    JsonNode chatEvent = event.at("/chat");
    if(!chatEvent.at("/addedToSpacePayload").isEmpty()) {
      return new GenericJson() { {
        put("hostAppDataAction", new GenericJson() { {
          put("chatDataAction", new GenericJson() { {
            put("createMessageAction", new GenericJson() { {
              put("message", new Message().setText(
                "Hi, Cymbal at your service. I help you manage your calendar" +
                "from Google Chat. Take a look at your schedule today by typing" +
                "`/checkCalendar`, or schedule a meeting with `/scheduleMeeting`. " +
                "To learn what else I can do, type `/help`."
              ));
            } });
          } });
        } });
      } };
    }
  }
}
```

**Apps Script**

```javascript
/**
 * Sends an onboarding message when the Chat app is added to a space.
 *
 * @param {Object} event The event object from Chat API.
 * @return {Object} Response from the Chat app.
 */
function onAddedToSpace(event) {
  return { hostAppDataAction: { chatDataAction: { createMessageAction: { message: {
    text: 'Hi, Cymbal at your service. I help you manage your calendar' +
          'from Google Chat. Take a look at your schedule today by typing' +
          '`/checkCalendar`, or schedule a meeting with `/scheduleMeeting`. ' +
          'To learn what else I can do, type `/help`.'
  }}}}};
}
```

The code sample returns the following text message:

![Example onboarding message.](https://developers.google.com/static/workspace/add-ons/images/design-principles-onboarding-example-scheduler.png)

For additional examples of how to respond with a message, see the following
guides:

- [Respond to quick commands](https://developers.google.com/workspace/add-ons/chat/quick-commands)
- [Respond to slash commands](https://developers.google.com/workspace/add-ons/chat/slash-commands)
- [Open interactive dialogs](https://developers.google.com/workspace/add-ons/chat/dialogs)
- [Collect information from Google Chat users](https://developers.google.com/workspace/add-ons/chat/collect-information)

## Update a message

Chat apps can also update messages they send. For example, to
update a message after a user has submitted a dialog or clicked a button in a
message.

To update a Chat app message, return the action
`DataActions` with a
[`UpdateMessageAction`](https://developers.google.com/workspace/add-ons/reference/rpc/apps.extensions.markup#updatemessageaction), as shown in
the following example:

```json
{ "hostAppDataAction": { "chatDataAction": { "updateMessageAction": {
  "message": MESSAGE
}}}}
```

Replace `MESSAGE` with a
[`Message`](https://developers.google.com/workspace/chat/api/reference/rest/v1/spaces.messages)
resource from the Chat API.

To learn more about how actions work, see
[Chat actions](https://developers.google.com/workspace/add-ons/chat/build#actions).

Chat apps can also update a message from a user to return a
preview of a link they sent. For details, see
[Preview links in Google Chat messages](https://developers.google.com/workspace/add-ons/chat/preview-links).

## Reply to interactions or send proactive messages using the Google Chat API

Instead of returning an add-on action,
Chat apps might need to use the Google Chat API respond to an
interaction. For example, Chat apps must call the Google Chat API to
do any of the following:

- Send messages on a schedule, or about changes to external resources. For
example, notifications about a new issue or case.
- Reply more than 30 seconds after the interaction. For example, to respond
with a message after completing a long-running task.
- Send a message outside of the space where the interaction took place.
- Send a message on behalf of a Chat user.

To send a message using the Chat API, you must set up authentication
and call the `create()` method on the `Message` resource. For steps, see
[Send a message using the Google Chat API](https://developers.google.com/workspace/chat/create-messages).

## Related topics

- [Build Google Chat interfaces](https://developers.google.com/workspace/add-ons/chat/build)
- [Respond to quick commands](https://developers.google.com/workspace/add-ons/chat/quick-commands)
- [Respond to slash commands](https://developers.google.com/workspace/add-ons/chat/slash-commands)
- [Open interactive dialogs](https://developers.google.com/workspace/add-ons/chat/dialogs)
- [Collect information from Google Chat users](https://developers.google.com/workspace/add-ons/chat/collect-information)
- [Preview links in Google Chat messages](https://developers.google.com/workspace/add-ons/chat/preview-links)
- [Send a message using the Google Chat API](https://developers.google.com/workspace/chat/create-messages)
