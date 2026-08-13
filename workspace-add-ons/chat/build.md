# Build Google Chat interfaces

## Page Summary

- This guide explains how to build user interfaces for Google Workspace add-ons that extend Google Chat, enabling interactive functionality within Chat spaces.
- Google Chat add-ons utilize triggers like adding to space, messages, and removal to initiate actions and responses.
- Developers can use event objects to access data from user interactions and triggers within their Chat add-ons.
- Chat apps can respond to interactions with various actions, including sending messages, displaying cards, and opening dialogs.
- Add-ons can leverage the Google Chat API for advanced functionalities like delayed responses, cross-space operations, or user authentication.

This page provides an overview of how to build user interfaces
(UIs) for Google Workspace add-ons that extend Google Chat.

**Note:** In Google Chat, add-ons appear to users as
Google Chat apps. You can also build your Chat app using 
*Google Chat API interaction events*. To learn more, see the
[Extend Google Chat overview](https://developers.google.com/workspace/add-ons/chat).

To build interfaces for Chat apps, you use the following
add-on components:

- Triggers: The ways that Google Chat users can invoke a
Chat app, such as adding it to a space or sending
it a message.
- Event objects: The data that Chat apps
receive from triggers or UI interactions.
- Actions: The ways that Chat apps can respond to
interactions, such as sending messages or returning a card-based user
interface.

![Chat app receives an event object from an Added to space trigger](https://developers.google.com/static/workspace/add-ons/images/design-principles-onboarding-example-scheduler.png)

Chat apps can build and display cards in the following
interfaces:

- [Messages](https://developers.google.com/workspace/add-ons/chat/send-messages) that can contain text,
static or interactive cards, and buttons.
- [Dialogs](https://developers.google.com/workspace/add-ons/chat/dialogs) which are cards that open in a new
window and typically prompt users to submit information.
- [Link previews](https://developers.google.com/workspace/add-ons/chat/preview-links) which are cards that
preview information about an external service.

## Triggers

This section explains the triggers that Google Workspace add-ons use in
Chat.

[Triggers](https://developers.google.com/workspace/add-ons/concepts/workspace-triggers) are the specific ways
that users invoke a Chat app using the
Chat UI, such as using @mentions or app commands.

The following table shows Chat triggers, a description, and how
Chat apps typically respond:

| Trigger | Description | Typical response |
|---|---|---|
| **Added to space** | A user adds the Chat app to a space, or a Google Workspace administrator installs the Chat app in direct message spaces for users in their organization. To learn about Chat apps installed by administrators, see [Install Marketplace apps in your domain](https://support.google.com/a/answer/172482) in the Google Workspace Admin Help documentation. | The Chat app sends an onboarding message that explains what it does and how users in the space can interact with it. |
| **Message** | A user interacts with the Chat app in a message one of the following ways: Sends a message in a direct message (DM) space with the Chat app. @mentions the Chat app in any type of space. Sends a message that contains a link that matches the URL pattern for [link previews](https://developers.google.com/workspace/add-ons/chat/preview-links). Types text into the multiselect menu of a [`selectionInput`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#google.apps.card.v1.SelectionInput) widget. | The Chat app responds based on the content of the message. For example, a Chat app replies to the slash command `/about` with a message that explains the tasks that the Chat app can do. |
| **Removed from space** | A user removes the Chat app from a space, or a Google Workspace administrator uninstalls the Chat app for a user in their organization. Users can't remove Chat apps that were installed by their administrator. If a user had previously installed the Chat app, Chat app remains installed regardless of whether an Google Workspace administrator tries to uninstall. | The Chat app removes any incoming notifications configured for the space (such as deleting a webhook) and clears up any internal storage. Chat apps can't respond with messages to this trigger, because they're no longer a member of the space. |
| **App command** | A user uses a [Chat app command](https://developers.google.com/workspace/add-ons/chat/commands). | The Chat app responds to the command. For example, replies with a message or opens a dialog. |

Unlike other add-ons, you must configure any callback functions
for these triggers using the Google Chat API. For guidance, see [Configure a
Chat app](https://developers.google.com/workspace/add-ons/chat/configure).

To respond to a trigger, see the following guides:

- [Send Google Chat messages](https://developers.google.com/workspace/add-ons/chat/send-messages)
- [Open interactive dialogs](https://developers.google.com/workspace/add-ons/chat/dialogs)
- [Preview links in Google Chat messages](https://developers.google.com/workspace/add-ons/chat/preview-links)

## Event objects

Chat apps receive event objects when a Chat
trigger fires, or when Chat users interact with a UI from the
Chat app (such as clicking a button). The event object
lets you use interaction data to respond or update a UI.

To learn about handling event objects, see the following guides:

- [Send Google Chat messages](https://developers.google.com/workspace/add-ons/chat/send-messages)
- [Open interactive dialogs](https://developers.google.com/workspace/add-ons/chat/dialogs)
- [Preview links in Google Chat messages](https://developers.google.com/workspace/add-ons/chat/preview-links)

To learn about add-on event objects within
Chat and other Google Workspace applications, see
[Event objects](https://developers.google.com/workspace/add-ons/concepts/event-objects).

## Chat actions

This section explains how Chat apps can use
[add-on actions](https://developers.google.com/workspace/add-ons/concepts/actions)
to respond to user interactions.

To respond with an add-on action, a
Chat app must respond within 30 seconds, and the
response must be posted in the space where the interaction occurred.
Otherwise, the Chat app must set up authentication and
call the Google Chat API to respond.

Chat apps can handle and respond to interactions in many ways.
In many cases,
Chat apps reply with a message.
Chat apps can also look up some information from a data
source, record the event object information, or just about anything else.
This processing behavior is essentially what defines the
Google Chat app.

To respond to user interactions, Chat apps must handle the
corresponding event object and return one of the following JSON objects:

- [`DataActions`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#google.apps.card.v1.DataActions): Creates or updates
Google Workspace data. To
[send or update Chat messages](https://developers.google.com/workspace/add-ons/chat/send-messages),
the object must contain the markup that defines the changes to the `Message`
data, represented as
[`chatDataActionMarkup`](https://developers.google.com/workspace/add-ons/reference/rpc/apps.extensions.markup#chatdataactionmarkup).
- [`RenderActions`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#renderactions): Create or Update a
[dialog](https://developers.google.com/workspace/add-ons/chat/dialogs) or provide input suggestions for a
[multi-select menu](https://developers.google.com/workspace/add-ons/chat/collect-information#add-multiselect).
- [`AuthorizationError`](https://developers.google.com/workspace/add-ons/guides/connect-third-party-service#build_and_return_a_sign-in_card):
Prompts users with an authorization card to sign in or authenticate to a
service that's external to Google. In Chat, only
[basic authorization card](https://developers.google.com/workspace/add-ons/guides/connect-third-party-service#basic-auth-card)
is supported.

The following table shows how Chat apps can respond with
actions. Chat apps can return JSON objects or build the
response using Apps Script's
[`AddOnResponseService`](https://developers.google.com/apps-script/reference/add-ons-response-service/add-ons-response-service).

| Chat app response | Required action to return (JSON) | Required action to return (Apps Script) |
|---|---|---|
| [Send or update a message](https://developers.google.com/workspace/add-ons/chat/send-messages) . | `DataActions` | `DataActionsResponse` |
| Open, update, or close a [dialog](https://developers.google.com/workspace/add-ons/chat/dialogs) . | `RenderActions` | `ActionResponse` |
| To [collect information](https://developers.google.com/workspace/add-ons/chat/collect-information) from a card or dialog, suggest selection items based on what users type into a multiselect menu. | `RenderActions` | `ActionResponse` |
| [Preview links](https://developers.google.com/workspace/add-ons/chat/preview-links) in messages that Chat users send in a space. | `DataActions` | `DataActionsResponse` |

### Respond using the Google Chat API

Instead of returning an add-on action,
Chat apps might need to use the Google Chat API respond to an
interaction. For example, Chat apps must call the Google Chat API to
do any of the following:

- Respond to an interaction after 30 seconds.
- Perform tasks outside of the space where the interaction took place.
- Perform tasks in Chat that aren't available as
add-on actions. For example, list spaces that a user
or Chat app is a member of, or add users to space.
- Perform tasks on behalf of the Chat user (which requires
user authentication).

When responding to an interaction event after 30 seconds, to avoid a
user-facing error message saying your Chat app isn't
responding, you must acknowledge receipt of an interaction event within 30
seconds by sending an empty response, as shown here:

**Node.js**

```javascript
async function onEvent(req, res) {
  // Trigger asynchronous job that will respond using the Google Chat API.
  ...

  // Respond with an empty response to the Google Chat platform.
  return res.send({});
};
```

**Python**

```python
def on_event(event) -> dict:
  # Trigger asynchronous job that will respond using the Google Chat API.
  ...

  # Respond with an empty response to the Google Chat platform.
  return {}
```

**Java**

```java
public String onEvent(JsonNode event) {
  // Trigger asynchronous job that will respond using the Google Chat API.
  ...

  // Respond with an empty response to the Google Chat platform.
  return "{}";
}
```

**Apps Script**

```javascript
function onEvent(event) {
  // Trigger asynchronous job that will respond using the Google Chat API.
  ...

  // Respond with an empty response to the Google Chat platform.
  return null;
}
```

To learn about authenticating and calling the Chat API, see the
[Chat API overview](https://developers.google.com/workspace/chat/api-overview).

## Related topics

- [Triggers for Google Workspace add-ons](https://developers.google.com/workspace/add-ons/concepts/workspace-triggers)
- [Configure a Google Chat app](https://developers.google.com/workspace/add-ons/chat/configure)
- [Event objects](https://developers.google.com/workspace/add-ons/concepts/event-objects)
- [Add-on actions](https://developers.google.com/workspace/add-ons/concepts/actions)
- [Send Google Chat messages](https://developers.google.com/workspace/add-ons/chat/send-messages)
- [Open interactive dialogs](https://developers.google.com/workspace/add-ons/chat/dialogs)
- [Preview links in Google Chat messages](https://developers.google.com/workspace/add-ons/chat/preview-links)
- [Chat API overview](https://developers.google.com/workspace/chat/api-overview)
