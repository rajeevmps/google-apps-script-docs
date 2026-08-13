# Preview links in Google Chat messages

## Page Summary

- Google Chat apps can display custom previews for shared links based on defined URL patterns, enhancing user experience with context and interactive elements.

- Developers can configure up to 5 URL patterns per app, with previews generated for the first HTTPS link in a message; subsequent links and non-HTTPS links are disregarded.

- Upon user interaction with the preview card, such as clicking a button, the app can dynamically update the card's content using designated actions.

- Link previews are visible to all users within the Google Chat space where the link is shared, ensuring consistent information access.

- Apps can utilize Node.js or Apps Script to handle link preview interactions, providing flexibility in development and implementation.

To prevent context switching when users share a link in Google Chat, your Chat app can _preview_ the link by attaching a card to their message that gives more information and lets people take action right from Google Chat.

**Note:** In Google Chat, add-ons appear to users as Google Chat apps. You can also build your Chat app using _Google Chat API interaction events_. To learn more, see the [Extend Google Chat overview](/workspace/add-ons/chat).

For example, imagine a Google Chat space that includes all of a company's customer service agents plus a Chat app named Case-y. Agents frequently share links to customer service cases in the Chat space, and each time they do their colleagues must open the case link to see details like assignee, status, and subject. Likewise, if someone wants to take ownership of a case or change the status, then they need to open the link.

Link previewing enables the space's resident Chat app, Case-y, to attach a card showing assignee, status, and subject whenever someone shares a case link. Buttons on the card let agents take ownership of the case and change the status directly from the chat stream.

## How link previewing works

When someone adds a link to their message, a chip appears which lets them know that a Chat app might preview the link.

![Chip indicating that a Chat app might preview a link](/static/workspace/add-ons/images/link-preview-chip.png)

After sending the message, the link is sent to the Chat app, which then generates and attaches the card to the user's message.

![Chat app previewing a link by attaching a card to the message](/static/workspace/add-ons/images/link-preview-case-details.png)

Alongside the link, the card provides additional information about the link, including interactive elements like buttons. Your Chat app can update the attached card in response to user interactions, like button clicks.

If someone doesn't want the Chat app to preview their link by attaching a card to their message, they can prevent previewing by clicking cancel on the preview chip. Users can remove the attached card at any time by clicking **Remove preview**.

## Prerequisites

### HTTP

A Google Workspace add-on that extends Google Chat. To build one, complete the [HTTP quickstart](/workspace/add-ons/chat/quickstart-http).

**Note:** The code samples in this guide are written to run as a [Google Cloud Run function](https://cloud.google.com/functions/docs/quickstarts) for Node.js.

### Apps Script

A Google Workspace add-on that extends Google Chat. To build one, complete the [Apps Script quickstart](/workspace/add-ons/chat/quickstart-apps-script).

## Configure link previews

Register specific links - like `example.com`, `support.example.com`, and `support.example.com/cases/` - as URL patterns on your Chat app's configuration page in Google Cloud console so your Chat app can preview them.

![Link previews configuration menu](/static/workspace/add-ons/images/link-preview-configuration.png)

1.  Open the [Google Cloud console](https://console.cloud.google.com/).
2.  Next to "Google Cloud," click the Down arrow arrow_drop_down and open your Chat app's project.
3.  In the search field, type `Google Chat API` and click **Google Chat API**.
4.  Click **Manage > Configuration**.
5.  Under Link previews, add or edit a URL pattern.
    1.  To configure link previews for a new URL pattern, click **Add URL Pattern**.
    2.  To edit the configuration for an existing URL pattern, click the Down arrow expand_more.
6.  In the **Host pattern** field, enter the domain of the URL pattern. The Chat app will preview links to this domain.

    To have the Chat app preview links for a specific subdomain, like `subdomain.example.com`, include the subdomain.

    To have the Chat app preview links for the entire domain, specify a wildcard character with an asterisk (*) as the subdomain. For example, `*.example.com` matches `subdomain.example.com` and `any.number.of.subdomains.example.com`.

7.  In the **Path prefix** field, enter a path to append to the host pattern domain.

    To match all URLs in the host pattern domain, leave **Path prefix** empty.

    For example, if the Host pattern is `support.example.com`, to match URLs for cases hosted at `support.example.com/cases/`, enter `cases/`.

8.  Click **Done**.

9.  Click **Save**.

Now, whenever someone includes a link that matches a link preview URL pattern to a message in a Chat space that includes your Chat app, your app previews the link.

## Preview a link

After you configure link previewing for a given link, your Chat app can recognize and preview the link by attaching more information to it.

Inside Chat spaces that include your Chat app, when someone's message contains a link that matches a link preview URL pattern, your Chat app receives an [event object](/workspace/add-ons/chat/build#event-objects) with a [`MessagePayload`](/workspace/add-ons/concepts/event-objects#messagepayload). In the payload, the [`message.matchedUrl`](/workspace/chat/api/reference/rest/v1/spaces.messages#matchedurl) object contains the link that the user included in the message:

### JSON

```json
message: {
      matchedUrl: {
        url: "https://support.example.com/cases/case123"
      },
      ... // other message attributes redacted
    }
```

By checking for the presence of the `matchedUrl` field in the `MESSAGE` event payload, your Chat app can add information to the message with the previewed link. Your Chat app can either reply with a basic text message or attach a card.

### Reply with a text message

For basic responses, your Chat app can preview a link by replying with a text message to a link. This example attaches a message that repeats the link URL that matches a link preview URL pattern.

#### Node.js

File: `node/chat/preview-link/index.js`

```javascript
// Reply with a text message for URLs of the subdomain "text"
if (chatMessage.matchedUrl.url.includes("text.example.com")) {
  return { hostAppDataAction: { chatDataAction: { createMessageAction: { message: {
    text: 'event.chat.messagePayload.message.matchedUrl.url: ' + chatMessage.matchedUrl.url
  }}}}};
}
```

Replace `FUNCTION_URL` with the HTTP endpoint that handles button clicks.

#### Python

File: `python/chat/preview-link/main.py`

```python
# Reply with a text message for URLs of the subdomain "text"
if "text.example.com" in chatMessage.get('matchedUrl').get('url'):
  return { 'hostAppDataAction': { 'chatDataAction': { 'createMessageAction': { 'message': {
    'text': 'event.chat.messagePayload.message.matchedUrl.url: ' + chatMessage.get('matchedUrl').get('url')
  }}}}}
```

Replace `FUNCTION_URL` with the HTTP endpoint that handles button clicks.

#### Java

File: `java/chat/preview-link/src/main/java/com/google/chat/previewLink/App.java`

```java
// Reply with a text message for URLs of the subdomain "text"
if (chatMessage.at("/matchedUrl/url").asText().contains("text.example.com")) {
  return new GenericJson() {{
    put("hostAppDataAction", new GenericJson() {{
      put("chatDataAction", new GenericJson() {{
        put("createMessageAction", new GenericJson() {{
          put("message", new Message()
            .setText("event.chat.messagePayload.message.matchedUrl.url: " + chatMessage.at("/matchedUrl/url").asText()));
        }});
      }});
    }});
  }};
}
```

Replace `FUNCTION_URL` with the HTTP endpoint that handles button clicks.

#### Apps Script

File: `apps-script/chat/preview-link/preview-link.gs`

```javascript
// Reply with a text message for URLs of the subdomain "text".
if (chatMessage.matchedUrl.url.includes("text.example.com")) {
  return { hostAppDataAction: { chatDataAction: { createMessageAction: { message: {
    text: 'event.chat.messagePayload.message.matchedUrl.url: ' + chatMessage.matchedUrl.url
  }}}}};
}
```

### Attach a card that previews the link

To attach a card to a previewed link, return the action [`DataActions`](/workspace/add-ons/reference/rpc/google.apps.card.v1#google.apps.card.v1.DataActions) with the `ChatDataActionMarkup` object of type [`UpdateInlinePreviewAction`](/workspace/add-ons/reference/rpc/apps.extensions.markup#updateinlinepreviewaction).

In the following example, a Chat app adds a preview card to messages that contain the URL pattern `support.example.com`.

![Chat app previewing a link by attaching a card to the message](/static/workspace/add-ons/images/link-preview-case-details.png)

#### Node.js

File: `node/chat/preview-link/index.js`

```javascript
// Attach a card to the message for URLs of the subdomain "support"
if (chatMessage.matchedUrl.url.includes("support.example.com")) {
  // A hard-coded card is used in this example. In a real-life scenario,
  // the case information would be fetched and used to build the card.
  return { hostAppDataAction: { chatDataAction: { updateInlinePreviewAction: { cardsV2: [{
    cardId: 'attachCard',
    card: {
      header: {
        title: 'Example Customer Service Case',
        subtitle: 'Case basics',
      },
      sections: [{ widgets: [
      { decoratedText: { topLabel: 'Case ID', text: 'case123'}},
      { decoratedText: { topLabel: 'Assignee', text: 'Charlie'}},
      { decoratedText: { topLabel: 'Status', text: 'Open'}},
      { decoratedText: { topLabel: 'Subject', text: 'It won\'t turn on...' }},
      { buttonList: { buttons: [{
        text: 'OPEN CASE',
        onClick: { openLink: {
          url: 'https://support.example.com/orders/case123'
        }},
      }, {
        text: 'RESOLVE CASE',
        onClick: { openLink: {
          url: 'https://support.example.com/orders/case123?resolved=y',
        }},
      }, {
        text: 'ASSIGN TO ME',
        onClick: { action: { function: FUNCTION_URL }}
      }]}}
      ]}]
    }
  }]}}}};
}
```

Replace `FUNCTION_URL` with the HTTP endpoint that handles button clicks.

#### Python

File: `python/chat/preview-link/main.py`

```python
# Attach a card to the message for URLs of the subdomain "support"
if "support.example.com" in chatMessage.get('matchedUrl').get('url'):
  # A hard-coded card is used in this example. In a real-life scenario,
  # the case information would be fetched and used to build the card.
  return { 'hostAppDataAction': { 'chatDataAction': { 'updateInlinePreviewAction': { 'cardsV2': [{
    'cardId': 'attachCard',
    'card': {
      'header': {
        'title': 'Example Customer Service Case',
        'subtitle': 'Case basics',
      },
      'sections': [{ 'widgets': [
      { 'decoratedText': { 'topLabel': 'Case ID', 'text': 'case123'}},
      { 'decoratedText': { 'topLabel': 'Assignee', 'text': 'Charlie'}},
      { 'decoratedText': { 'topLabel': 'Status', 'text': 'Open'}},
      { 'decoratedText': { 'topLabel': 'Subject', 'text': 'It won\'t turn on...' }},
      { 'buttonList': { 'buttons': [{
        'text': 'OPEN CASE',
        'onClick': { 'openLink': {
          'url': 'https://support.example.com/orders/case123'
        }},
      }, {
        'text': 'RESOLVE CASE',
        'onClick': { 'openLink': {
          'url': 'https://support.example.com/orders/case123?resolved=y',
        }},
      }, {
        'text': 'ASSIGN TO ME',
        'onClick': { 'action': { 'function': FUNCTION_URL }}
      }]}}
      ]}]
    }
  }]}}}}
```

Replace `FUNCTION_URL` with the HTTP endpoint that handles button clicks.

#### Java

File: `java/chat/preview-link/src/main/java/com/google/chat/previewLink/App.java`

```java
// Attach a card to the message for URLs of the subdomain "support"
if (chatMessage.at("/matchedUrl/url").asText().contains("support.example.com")) {
  // A hard-coded card is used in this example. In a real-life scenario,
  // the case information would be fetched and used to build the card.
  CardWithId cardV2 = new CardWithId()
    .setCardId("attachCard")
    .setCard(new GoogleAppsCardV1Card()
      .setHeader(new GoogleAppsCardV1CardHeader()
        .setTitle("Example Customer Service Case")
        .setSubtitle("Case basics"))
      .setSections(List.of(new GoogleAppsCardV1Section().setWidgets(List.of(
        new GoogleAppsCardV1Widget().setDecoratedText(new GoogleAppsCardV1DecoratedText()
          .setTopLabel("Case ID")
          .setText("case123")),
        new GoogleAppsCardV1Widget().setDecoratedText(new GoogleAppsCardV1DecoratedText()
          .setTopLabel("Assignee")
          .setText("Charlie")),
        new GoogleAppsCardV1Widget().setDecoratedText(new GoogleAppsCardV1DecoratedText()
          .setTopLabel("Status")
          .setText("Open")),
        new GoogleAppsCardV1Widget().setDecoratedText(new GoogleAppsCardV1DecoratedText()
          .setTopLabel("Subject")
          .setText("It won't turn on...")),
        new GoogleAppsCardV1Widget().setButtonList(new GoogleAppsCardV1ButtonList()
          .setButtons(List.of(
            new GoogleAppsCardV1Button()
              .setText("OPEN CASE")
            .setOnClick(new GoogleAppsCardV1OnClick()
                .setOpenLink(new GoogleAppsCardV1OpenLink()
                  .setUrl("https://support.example.com/orders/case123"))),
            new GoogleAppsCardV1Button()
              .setText("RESOLVE CASE")
            .setOnClick(new GoogleAppsCardV1OnClick()
                .setOpenLink(new GoogleAppsCardV1OpenLink()
                  .setUrl("https://support.example.com/orders/case123?resolved=y"))),
            new GoogleAppsCardV1Button()
              .setText("ASSIGN TO ME")
              .setOnClick(new GoogleAppsCardV1OnClick()
                .setAction(new GoogleAppsCardV1Action().setFunction(FUNCTION_URL)))
          ))
        )
      ))))
    );

  return new GenericJson() {{
    put("hostAppDataAction", new GenericJson() {{
      put("chatDataAction", new GenericJson() {{
        put("updateInlinePreviewAction", new GenericJson() {{
          put("cardsV2", List.of(cardV2));
        }});
      }});
    }});
  }};
}
```

Replace `FUNCTION_URL` with the HTTP endpoint that handles button clicks.

#### Apps Script

File: `apps-script/chat/preview-link/preview-link.gs`

```javascript
// Attach a card to the message for URLs of the subdomain "support".
if (chatMessage.matchedUrl.url.includes("support.example.com")) {
  // A hard-coded card is used in this example. In a real-life scenario,
  // the case information would be fetched and used to build the card.
  return { hostAppDataAction: { chatDataAction: { updateInlinePreviewAction: { cardsV2: [{
    cardId: 'attachCard',
    card: {
      header: {
        title: 'Example Customer Service Case',
        subtitle: 'Case summary',
      },
      sections: [{ widgets: [
      { decoratedText: { topLabel: 'Case ID', text: 'case123'}},
      { decoratedText: { topLabel: 'Assignee', text: 'Charlie'}},
      { decoratedText: { topLabel: 'Status', text: 'Open'}},
      { decoratedText: { topLabel: 'Subject', text: 'It won\'t turn on...' }},
      { buttonList: { buttons: [{
        text: 'OPEN CASE',
        onClick: { openLink: {
          url: 'https://support.example.com/orders/case123'
        }},
      }, {
        text: 'RESOLVE CASE',
        onClick: { openLink: {
          url: 'https://support.example.com/orders/case123?resolved=y',
        }},
      }, {
        text: 'ASSIGN TO ME',
        // Clicking this button triggers the execution of the function
        // "assign" from the Apps Script project.
        onClick: { action: { function: 'assign'}}
      }]}}
      ]}]
    }
  }]}}}};
}
```

### Update a link preview card

Your Chat app can update a link preview card when users interact with it, such as clicking a button on the card.

To update the card, your Chat app must return the action [`DataActions`](/workspace/add-ons/reference/rpc/google.apps.card.v1#google.apps.card.v1.DataActions) with one of the following `ChatDataActionMarkup` objects:

*   If a user sent the message, return an [`UpdateMessageAction`](/workspace/add-ons/reference/rpc/apps.extensions.markup#updatemessageaction) object.
*   If the Chat app sent the message, return an [`UpdateInlinePreviewAction`](/workspace/add-ons/reference/rpc/apps.extensions.markup#updateinlinepreviewaction) object.

To determine who sent the message, use the event payload ([`buttonClickedPayload`](/workspace/add-ons/concepts/event-objects#buttonclickedpayload)) to check whether the sender (`message.sender.type`) is set to `HUMAN` (user) or `BOT` (Chat app).

The following example shows how a Chat app updates a link preview whenever a user clicks the **Assign to Me** button by updating the card's **Assignee** field and disabling the button.

![Chat app previewing a link with an updated version of a card attached to the a message](/static/workspace/add-ons/images/link-preview-case-details-updated.png)

#### Node.js

File: `node/chat/preview-link/index.js`

```javascript
/**
 * Respond to clicks by assigning and updating the card that's attached to a
 * message previewed link of the pattern "support.example.com".
 *
 * @param {Object} chatMessage The chat message object from Google Workspace Add On event.
 * @return {Object} Action response depending on the message author.
 */
function handleCardClick(chatMessage) {
  // Creates the updated card that displays "You" for the assignee
  // and that disables the button.
  //
  // A hard-coded card is used in this example. In a real-life scenario,
  // an actual assign action would be performed before building the card.
  const message = { cardsV2: [{
    cardId: 'attachCard',
    card: {
      header: {
        title: 'Example Customer Service Case',
        subtitle: 'Case basics',
      },
      sections: [{ widgets: [
        { decoratedText: { topLabel: 'Case ID', text: 'case123'}},
        // The assignee is now "You"
        { decoratedText: { topLabel: 'Assignee', text: 'You'}},
        { decoratedText: { topLabel: 'Status', text: 'Open'}},
        { decoratedText: { topLabel: 'Subject', text: 'It won\'t turn on...' }},
        { buttonList: { buttons: [{
          text: 'OPEN CASE',
          onClick: { openLink: {
            url: 'https://support.example.com/orders/case123'
          }},
        }, {
          text: 'RESOLVE CASE',
          onClick: { openLink: {
            url: 'https://support.example.com/orders/case123?resolved=y',
          }},
        }, {
          text: 'ASSIGN TO ME',
          // The button is now disabled
          disabled: true,
          onClick: { action: { function: FUNCTION_URL }}
        }]}}
      ]}]
    }
  }]};

  // Use the adequate action response type. It depends on whether the message
  // the preview link card is attached to was created by a human or a Chat app.
  if(chatMessage.sender.type === 'HUMAN') {
    return { hostAppDataAction: { chatDataAction: { updateInlinePreviewAction: message }}};
  } else {
    return { hostAppDataAction: { chatDataAction: { updateMessageAction: message }}};
  }
}
```

Replace `FUNCTION_URL` with the HTTP endpoint that handles button clicks.

#### Python

File: `python/chat/preview-link/main.py`

```python
def handle_card_click(chatMessage: dict) -> dict:
  """Respond to clicks by assigning and updating the card that's attached to a
  message previewed link of the pattern "support.example.com".

  - Reply with text messages that echo "text.example.com" link URLs in messages.
  - Attach cards to messages with "support.example.com" link URLs.

  Args:
      chatMessage (Mapping[str, Any]): The chat message object from Google Workspace Add On event.

  Returns:
      Mapping[str, Any]: Action response depending on the message author.
  """
  # Creates the updated card that displays "You" for the assignee
  # and that disables the button.
  #
  # A hard-coded card is used in this example. In a real-life scenario,
  # an actual assign action would be performed before building the card.
  message = { 'cardsV2': [{
    'cardId': 'attachCard',
    'card': {
      'header': {
        'title': 'Example Customer Service Case',
        'subtitle': 'Case basics',
      },
      'sections': [{ 'widgets': [
      { 'decoratedText': { 'topLabel': 'Case ID', 'text': 'case123'}},
      # The assignee is now "You"
      { 'decoratedText': { 'topLabel': 'Assignee', 'text': 'You'}},
      { 'decoratedText': { 'topLabel': 'Status', 'text': 'Open'}},
      { 'decoratedText': { 'topLabel': 'Subject', 'text': 'It won\'t turn on...' }},
      { 'buttonList': { 'buttons': [{
        'text': 'OPEN CASE',
        'onClick': { 'openLink': {
          'url': 'https://support.example.com/orders/case123'
        }},
      }, {
        'text': 'RESOLVE CASE',
        'onClick': { 'openLink': {
          'url': 'https://support.example.com/orders/case123?resolved=y',
        }},
      }, {
        'text': 'ASSIGN TO ME',
        # The button is now disabled
        'disabled': True,
        'onClick': { 'action': { 'function': FUNCTION_URL }}
      }]}}
      ]}]
    }
  }]}

  # Use the adequate action response type. It depends on whether the message
  # the preview link card is attached to was created by a human or a Chat app.
  if chatMessage.get('sender').get('type') == 'HUMAN':
    return { 'hostAppDataAction': { 'chatDataAction': { 'updateInlinePreviewAction': message }}}
  else:
    return { 'hostAppDataAction': { 'chatDataAction': { 'updateMessageAction': message }}}
```

Replace `FUNCTION_URL` with the HTTP endpoint that handles button clicks.

#### Java

File: `java/chat/preview-link/src/main/java/com/google/chat/previewLink/App.java`

```java
/**
 * Respond to clicks by assigning and updating the card that's attached to a
 * message previewed link of the pattern "support.example.com".
 *
 * @param chatMessage The chat message object from Google Workspace Add On event.
 * @return Action response depending on the message author.
 */
GenericJson handleCardClick(JsonNode chatMessage) {
  // Creates the updated card that displays "You" for the assignee
  // and that disables the button.
  //
  // A hard-coded card is used in this example. In a real-life scenario,
  // an actual assign action would be performed before building the card.
  Message message = new Message().setCardsV2(List.of(new CardWithId()
    .setCardId("attachCard")
    .setCard(new GoogleAppsCardV1Card()
      .setHeader(new GoogleAppsCardV1CardHeader()
        .setTitle("Example Customer Service Case")
        .setSubtitle("Case basics"))
      .setSections(List.of(new GoogleAppsCardV1Section().setWidgets(List.of(
        new GoogleAppsCardV1Widget().setDecoratedText(new GoogleAppsCardV1DecoratedText()
          .setTopLabel("Case ID")
          .setText("case123")),
        // The assignee is now "You"
        new GoogleAppsCardV1Widget().setDecoratedText(new GoogleAppsCardV1DecoratedText()
          .setTopLabel("Assignee")
          .setText("You")),
        new GoogleAppsCardV1Widget().setDecoratedText(new GoogleAppsCardV1DecoratedText()
          .setTopLabel("Status")
          .setText("Open")),
        new GoogleAppsCardV1Widget().setDecoratedText(new GoogleAppsCardV1DecoratedText()
          .setTopLabel("Subject")
          .setText("It won't turn on...")),
        new GoogleAppsCardV1Widget().setButtonList(new GoogleAppsCardV1ButtonList()
          .setButtons(List.of(
            new GoogleAppsCardV1Button()
              .setText("OPEN CASE")
              .setOnClick(new GoogleAppsCardV1OnClick()
                .setOpenLink(new GoogleAppsCardV1OpenLink()
                  .setUrl("https://support.example.com/orders/case123"))),
            new GoogleAppsCardV1Button()
              .setText("RESOLVE CASE")
              .setOnClick(new GoogleAppsCardV1OnClick()
                .setOpenLink(new GoogleAppsCardV1OpenLink()
                  .setUrl("https://support.example.com/orders/case123?resolved=y"))),
            new GoogleAppsCardV1Button()
              .setText("ASSIGN TO ME")
              // The button is now disabled
              .setDisabled(true)
              .setOnClick(new GoogleAppsCardV1OnClick()
                .setAction(new GoogleAppsCardV1Action().setFunction(FUNCTION_URL)))
          ))
        )
      ))))
    )
  ));

  // Use the adequate action response type. It depends on whether the message
  // the preview link card is attached to was created by a human or a Chat app.
  if("HUMAN".equals(chatMessage.at("/sender/type").asText())) {
    return new GenericJson() {{
      put("hostAppDataAction", new GenericJson() {{
        put("chatDataAction", new GenericJson() {{
          put("updateInlinePreviewAction", message);
        }});
      }});
    }};
  } else {
    return new GenericJson() {{
      put("hostAppDataAction", new GenericJson() {{
        put("chatDataAction", new GenericJson() {{
          put("updateMessageAction", message);
        }});
      }});
    }};
  }
}
```

Replace `FUNCTION_URL` with the HTTP endpoint that handles button clicks.

#### Apps Script

File: `apps-script/chat/preview-link/preview-link.gs`

```javascript
/**
 * Assigns and updates the card that's attached to a message with a
 * previewed link of the pattern "support.example.com".
 *
 * @param {Object} event The event object from the Google Workspace add-on.
 * @return {Object} Action response depending on the message author.
 */
function assign(event) {
  // Creates the updated card that displays "You" for the assignee
  // and that disables the button.
  //
  // A hard-coded card is used in this example. In a real-life scenario,
  // an actual assign action would be performed before building the card.
  const message = { cardsV2: [{
    cardId: 'attachCard',
    card: {
      header: {
        title: 'Example Customer Service Case',
        subtitle: 'Case summary',
      },
      sections: [{ widgets: [
        { decoratedText: { topLabel: 'Case ID', text: 'case123'}},
        // The assignee is now "You"
        { decoratedText: { topLabel: 'Assignee', text: 'You'}},
        { decoratedText: { topLabel: 'Status', text: 'Open'}},
        { decoratedText: { topLabel: 'Subject', text: 'It won\'t turn on...' }},
        { buttonList: { buttons: [{
          text: 'OPEN CASE',
          onClick: { openLink: {
            url: 'https://support.example.com/orders/case123'
          }},
        }, {
          text: 'RESOLVE CASE',
          onClick: { openLink: {
            url: 'https://support.example.com/orders/case123?resolved=y',
          }},
        }, {
          text: 'ASSIGN TO ME',
          // The button is now disabled
          disabled: true,
          onClick: { action: { function: 'assign'}}
        }]}}
      ]}]
    }
  }]};

  // Use the adequate action response type. It depends on whether the message
  // the preview link card is attached to was created by a human or a Chat app.
  if(event.chat.buttonClickedPayload.message.sender.type === 'HUMAN') {
    return { hostAppDataAction: { chatDataAction: { updateInlinePreviewAction: message }}};
  } else {
    return { hostAppDataAction: { chatDataAction: { updateMessageAction: message }}};
  }
}
```

## Limits and considerations

As you configure link previews for your Chat app, take note of these limits and considerations:

*   Each Chat app supports link previews for up to 5 URL patterns.
*   Chat apps preview one link per message. If multiple previewable links are present in a single message, only the first previewable link previews.
*   Chat apps only preview links that begin with `https://`, so `https://support.example.com/cases/` previews, but `support.example.com/cases/` does not.
*   Unless the message includes other information that gets sent to the Chat app, like a [slash command](/workspace/add-ons/chat/slash-commands), only the link URL is sent to the Chat app by link previews.
*   If a user posts the link, a Chat app can only update the link preview card if users interact with the card, such as with a button click. You can't call the Chat API's `update()` method on the `Message` resource to update a user's message asynchronously.
*   Chat apps must preview links for everyone in the space, so the message must omit the `privateMessageViewer` field.

## Debug link previews

As you implement link previews, you might need to debug your Chat app by reading the app's logs. To read the logs, visit the [Logs Explorer](https://console.cloud.google.com/logs/query) on Google Cloud console.
