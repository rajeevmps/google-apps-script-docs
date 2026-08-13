# Extend the message UI

Google Workspace add-ons that extend Gmail can provide a user interface when the user is reading messages. This lets add-ons to automate tasks that respond to message content, such as displaying, retrieving, or sending out additional information related to the message.

## Access the Google Workspace add-on message UI

There are two ways to view an add-on's message UI. The first way is to open a message while the add-on is already open (for example, when viewing the add-on homepage in the Gmail inbox window). The second way is to start the add-on while viewing a message.

Either case causes the add-on to execute the corresponding contextual trigger function, defined in the add-on manifest. The trigger also executes if the user switches to a different message while the add-on is still open. The contextual trigger function builds the message UI for that message, which Gmail then displays to the user.

## Build a message add-on

You can add message functionality to an add-on by following these general steps:

1. Add the appropriate fields to the add-on script project manifest, including the scopes required for message functionality. Be sure to add a conditional trigger field to the manifest, with a unconditional value of `{}`.
2. Implement a contextual trigger function that builds a message UI when the user selects the add-on in a message.
3. Implement associated functions needed to respond to the user's UI interactions.

## Contextual triggers

To provide users assistance when reading messages, add-ons can define a contextual trigger in their manifests. When the user opens a Gmail message (with the add-on open) that meets the trigger criteria the trigger fires. A fired trigger executes a contextual trigger function that constructs the add-on user interface and returns it for Gmail to display. At that point the user can begin interacting with it.

Contextual triggers are defined in your add-on's project manifest. The trigger definition tells Gmail which trigger function to fire under which conditions. For example, this manifest snippet sets an unconditional trigger that calls the trigger function `onGmailMessageOpen()` when a message is opened:

```json
{
...
"addOns": {

"common": {
...
},
"gmail": {
"contextualTriggers": [
{
"unconditional": {},
"onTriggerFunction": "onGmailMessageOpen"
}
],
...
},
...
}
...
}
```

The only contextual trigger type available is `unconditional`, which triggers for all emails regardless of content.

## Contextual trigger function

Every contextual trigger must have a corresponding trigger function that constructs your add-on's user interface. You specify this function in your manifest's `onTriggerFunction` field. You implement this function to accept an action event object argument and return either a single `Card` object or an array of `Card` objects.

When a contextual trigger fires for a given Gmail message, it calls this function and passes it an action event object. Often trigger functions use the message ID provided by this event object to get the message text and other details using Apps Script's Gmail service. In most cases you must activate Gmail scopes using the access token provided by the event object and the `GmailApp.setCurrentMessageAccessToken(accessToken)` function before using other Gmail service functions. For example, your trigger function could extract message content using these functions:

```javascript
// Activate temporary Gmail scopes, in this case to allow
// the add-on to read message metadata and content.
var accessToken = e.gmail.accessToken;
GmailApp.setCurrentMessageAccessToken(accessToken);

// Read message metadata and content. This requires the Gmail scope
// https://www.googleapis.com/auth/gmail.addons.current.message.readonly.
var messageId = e.gmail.messageId;
var message = GmailApp.getMessageById(messageId);
var subject = message.getSubject();
var sender = message.getFrom();
var body = message.getPlainBody();
var messageDate = message.getDate();

// Setting the access token with a gmail.addons.current.message.readonly
// scope also allows read access to the other messages in the thread.
var thread = message.getThread();
var threadMessages = thread.getMessages();

// Using this link can avoid the need to copy message or thread content
var threadLink = thread.getPermalink();
```

The trigger function can then act on this data, extracting the information that it needs for the interface. For example, an add-on that summarizes sales numbers can collect sales figures from the message body and organize them for display in a card.

The trigger function must build and return an array of built `Card` objects. For example, the following builds an add-on with a single card that just lists the subject and sender of the message:

```javascript
function onGmailMessageOpen(e) {
  // Activate temporary Gmail scopes, in this case to allow
  // message metadata to be read.
  var accessToken = e.gmail.accessToken;
  GmailApp.setCurrentMessageAccessToken(accessToken);

  var messageId = e.gmail.messageId;
  var message = GmailApp.getMessageById(messageId);
  var subject = message.getSubject();
  var sender = message.getFrom();

  // Create a card with a single card section and two widgets.
  // Be sure to execute build() to finalize the card construction.
  var exampleCard = CardService.newCardBuilder()
      .setHeader(CardService.newCardHeader()
          .setTitle('Example card'))
      .addSection(CardService.newCardSection()
          .addWidget(CardService.newDecoratedText()
              .setTopLabel('Subject')
              .setText(subject))
          .addWidget(CardService.newDecoratedText()
              .setTopLabel('From')
              .setText(sender)))
      .build(); // Don't forget to build the Card!
  return [exampleCard];
}
```
