# Build a Google Workspace add-on with Apps Script

- This guide details the creation of a Google Workspace add-on that displays a random cat image with text pulled from Gmail, Drive, or Calendar.
- The add-on uses Apps Script and requires a Google Cloud project for setup and deployment.
- Users interact with the add-on through cards displayed within Gmail, Drive, and Calendar interfaces.
- Functionality is triggered by specific actions like opening an email, selecting Drive items, or viewing a calendar event.
- The guide covers setup, configuration, deployment, and basic usage of the add-on.

## Overview

This quickstart creates a Google Workspace add-on that demonstrates homepages, contextual triggers, and connecting to third-party APIs.

The add-on creates contextual and non-contextual interfaces in Gmail, Calendar, and Drive. The add-on displays a random image of a cat with text overlaying the image. The text is either static for homepages or taken from the host application context for contextual triggers.

## Objectives

- Set up the script.
- Run the script.

## Prerequisites

To use this sample, you need the following prerequisites:

- A Google Account (Google Workspace accounts might require administrator approval).
- A web browser with access to the internet.

## Set up the script

To set up the quickstart, create the script project and install a test deployment.

### Create the Apps Script project

1. Go to [script.new](https://script.google.com/u/0/home/projects/create) to create a new Apps Script project.
2. Click **Untitled project**.
3. Rename the Apps Script project **Cats** and click **Rename**.
4. Next to the `Code.gs` file, click More more_vert > **Rename**. Name the file `Common`.
5. Click Add a file add > **Script**. Name the file `Gmail`.
6. Repeat step 5 to create 2 more script files named `Calendar` and `Drive`. When you're done you should have 4 separate script files.
7. Replace the contents of each file with the following corresponding code:

#### Common.gs

```javascript
/**
 * This simple Google Workspace add-on shows a random image of a cat in the
 * sidebar. When opened manually (the homepage card), some static text is
 * overlayed on the image, but when contextual cards are opened a new cat image
 * is shown with the text taken from that context (such as a message's subject
 * line) overlaying the image. There is also a button that updates the card with
 * a new random cat image.
 *
 * Click "File > Make a copy..." to copy the script, and "Publish > Deploy from
 * manifest > Install add-on" to install it.
 */

/**
 * The maximum number of characters that can fit in the cat image.
 */
var MAX_MESSAGE_LENGTH = 40;

/**
 * Callback for rendering the homepage card.
 * @return {CardService.Card} The card to show to the user.
 */
function onHomepage(e) {
  console.log(e);
  var hour = Number(Utilities.formatDate(new Date(), e.userTimezone.id, 'H'));
  var message;
  if (hour >= 6 && hour < 12) {
    message = 'Good morning';
  } else if (hour >= 12 && hour < 18) {
    message = 'Good afternoon';
  } else {
    message = 'Good night';
  }
  message += ' ' + e.hostApp;
  return createCatCard(message, true);
}

/**
 * Creates a card with an image of a cat, overlayed with the text.
 * @param {String} text The text to overlay on the image.
 * @param {Boolean} isHomepage True if the card created here is a homepage;
 *      false otherwise. Defaults to false.
 * @return {CardService.Card} The assembled card.
 */
function createCatCard(text, isHomepage) {
  // Explicitly set the value of isHomepage as false if null or undefined.
  if (!isHomepage) {
    isHomepage = false;
  }

  // Use the "Cat as a service" API to get the cat image. Add a "time" URL
  // parameter to act as a cache buster.
  var now = new Date();
  // Replace forward slashes in the text, as they break the CataaS API.
  var caption = text.replace(/\//g, ' ');
  var imageUrl =
      Utilities.formatString('https://cataas.com/cat/says/%s?time=%s',
          encodeURIComponent(caption), now.getTime());
  var image = CardService.newImage()
      .setImageUrl(imageUrl)
      .setAltText('Meow')

  // Create a button that changes the cat image when pressed.
  // Note: Action parameter keys and values must be strings.
  var action = CardService.newAction()
      .setFunctionName('onChangeCat')
      .setParameters({text: text, isHomepage: isHomepage.toString()});
  var button = CardService.newTextButton()
      .setText('Change cat')
      .setOnClickAction(action)
      .setTextButtonStyle(CardService.TextButtonStyle.FILLED);
  var buttonSet = CardService.newButtonSet()
      .addButton(button);

  // Create a footer to be shown at the bottom.
  var footer = CardService.newFixedFooter()
      .setPrimaryButton(CardService.newTextButton()
          .setText('Powered by cataas.com')
          .setOpenLink(CardService.newOpenLink()
              .setUrl('https://cataas.com')));

  // Assemble the widgets and return the card.
  var section = CardService.newCardSection()
      .addWidget(image)
      .addWidget(buttonSet);
  var card = CardService.newCardBuilder()
      .addSection(section)
      .setFixedFooter(footer);

  if (!isHomepage) {
    // Create the header shown when the card is minimized,
    // but only when this card is a contextual card. Peek headers
    // are never used by non-contexual cards like homepages.
    var peekHeader = CardService.newCardHeader()
      .setTitle('Contextual Cat')
      .setImageUrl('https://www.gstatic.com/images/icons/material/system/1x/pets_black_48dp.png')
      .setSubtitle(text);
    card.setPeekCardHeader(peekHeader)
  }

  return card.build();
}

/**
 * Callback for the "Change cat" button.
 * @param {Object} e The event object, documented {@link
 *     https://developers.google.com/gmail/add-ons/concepts/actions#action_event_objects
 *     here}.
 * @return {CardService.ActionResponse} The action response to apply.
 */
function onChangeCat(e) {
  console.log(e);
  // Get the text that was shown in the current cat image. This was passed as a
  // parameter on the Action set for the button.
  var text = e.parameters.text;

  // The isHomepage parameter is passed as a string, so convert to a Boolean.
  var isHomepage = e.parameters.isHomepage === 'true';

  // Create a new card with the same text.
  var card = createCatCard(text, isHomepage);

  // Create an action response that instructs the add-on to replace
  // the current card with the new one.
  var navigation = CardService.newNavigation()
      .updateCard(card);
  var actionResponse = CardService.newActionResponseBuilder()
      .setNavigation(navigation);
  return actionResponse.build();
}

/**
 * Truncate a message to fit in the cat image.
 * @param {string} message The message to truncate.
 * @return {string} The truncated message.
 */
function truncate(message) {
  if (message.length > MAX_MESSAGE_LENGTH) {
    message = message.slice(0, MAX_MESSAGE_LENGTH);
    message = message.slice(0, message.lastIndexOf(' ')) + '...';
  }
  return message;
}
```

#### Gmail.gs

```javascript
/**
 * Callback for rendering the card for a specific Gmail message.
 * @param {Object} e The event object.
 * @return {CardService.Card} The card to show to the user.
 */
function onGmailMessage(e) {
  console.log(e);
  // Get the ID of the message the user has open.
  var messageId = e.gmail.messageId;

  // Get an access token scoped to the current message and use it for GmailApp
  // calls.
  var accessToken = e.gmail.accessToken;
  GmailApp.setCurrentMessageAccessToken(accessToken);

  // Get the subject of the email.
  var message = GmailApp.getMessageById(messageId);
  var subject = message.getThread().getFirstMessageSubject();

  // Remove labels and prefixes.
  subject = subject
      .replace(/^(\[rR\]\[eE\]|\[fF\]\[wW\]\[dD\])\:\s*/, '')
      .replace(/^\[.*?\]\s*/, '');

  // If neccessary, truncate the subject to fit in the image.
  subject = truncate(subject);

  return createCatCard(subject);
}

/**
 * Callback for rendering the card for the compose action dialog.
 * @param {Object} e The event object.
 * @return {CardService.Card} The card to show to the user.
 */
function onGmailCompose(e) {
  console.log(e);
  var header = CardService.newCardHeader()
      .setTitle('Insert cat')
      .setSubtitle('Add a custom cat image to your email message.');
  // Create text input for entering the cat's message.
  var input = CardService.newTextInput()
      .setFieldName('text')
      .setTitle('Caption')
      .setHint('What do you want the cat to say?');
  // Create a button that inserts the cat image when pressed.
  var action = CardService.newAction()
      .setFunctionName('onGmailInsertCat');
  var button = CardService.newTextButton()
      .setText('Insert cat')
      .setOnClickAction(action)
      .setTextButtonStyle(CardService.TextButtonStyle.FILLED);
  var buttonSet = CardService.newButtonSet()
      .addButton(button);
  // Assemble the widgets and return the card.
  var section = CardService.newCardSection()
      .addWidget(input)
      .addWidget(buttonSet);
  var card = CardService.newCardBuilder()
      .setHeader(header)
      .addSection(section);
  return card.build();
}

/**
 * Callback for inserting a cat into the Gmail draft.
 * @param {Object} e The event object.
 * @return {CardService.UpdateDraftActionResponse} The draft update response.
 */
function onGmailInsertCat(e) {
  console.log(e);
  // Get the text that was entered by the user.
  var text = e.formInput.text;
  // Use the "Cat as a service" API to get the cat image. Add a "time" URL
  // parameter to act as a cache buster.
  var now = new Date();
  var imageUrl = 'https://cataas.com/cat';
  if (text) {
    // Replace forward slashes in the text, as they break the CataaS API.
    var caption = text.replace(/\//g, ' ');
    imageUrl += Utilities.formatString('/says/%s?time=%s',
        encodeURIComponent(caption), now.getTime());
  }
  var imageHtmlContent = '<img style="display: block; max-height: 300px;" src="'
      + imageUrl + '"/>';
  var response = CardService.newUpdateDraftActionResponseBuilder()
      .setUpdateDraftBodyAction(CardService.newUpdateDraftBodyAction()
          .addUpdateContent(imageHtmlContent,CardService.ContentType.MUTABLE_HTML)
          .setUpdateType(CardService.UpdateDraftBodyType.IN_PLACE_INSERT))
      .build();
  return response;
}
```

#### Calendar.gs

```javascript
/**
 * Callback for rendering the card for a specific Calendar event.
 * @param {Object} e The event object.
 * @return {CardService.Card} The card to show to the user.
 */
function onCalendarEventOpen(e) {
  console.log(e);
  var calendar = CalendarApp.getCalendarById(e.calendar.calendarId);
  // The event metadata doesn't include the event's title, so using the
  // calendar.readonly scope and fetching the event by it's ID.
  var event = calendar.getEventById(e.calendar.id);
  if (!event) {
    // This is a new event still being created.
    return createCatCard('A new event! Am I invited?');
  }
  var title = event.getTitle();
  // If necessary, truncate the title to fit in the image.
  title = truncate(title);
  return createCatCard(title);
}
```

#### Drive.gs

```javascript
/**
 * Callback for rendering the card for specific Drive items.
 * @param {Object} e The event object.
 * @return {CardService.Card} The card to show to the user.
 */
function onDriveItemsSelected(e) {
  console.log(e);
  var items = e.drive.selectedItems;
  // Include at most 5 items in the text.
  items = items.slice(0, 5);
  var text = items.map(function(item) {
    var title = item.title;
    // If neccessary, truncate the title to fit in the image.
    title = truncate(title);
    return title;
  }).join('\n');
  return createCatCard(text);
}
```

8. Click **Project Settings**.

9. Check the **Show "appsscript.json" manifest file in editor** box.

10. Click **Editor**.

11. Open the `appsscript.json` file and replace the contents with the following code, then click Save.

#### appsscript.json

```json
{
  "timeZone": "America/New_York",
  "dependencies": {
  },
  "exceptionLogging": "STACKDRIVER",
  "oauthScopes": [
    "https://www.googleapis.com/auth/calendar.addons.execute",
    "https://www.googleapis.com/auth/calendar.readonly",
    "https://www.googleapis.com/auth/drive.addons.metadata.readonly",
    "https://www.googleapis.com/auth/gmail.addons.current.action.compose",
    "https://www.googleapis.com/auth/gmail.addons.current.message.readonly",
    "https://www.googleapis.com/auth/gmail.addons.execute",
    "https://www.googleapis.com/auth/script.locale"
  ],
  "runtimeVersion": "V8",
  "addOns": {
    "common": {
      "name": "Cats",
      "logoUrl": "https://www.gstatic.com/images/icons/material/system/1x/pets_black_48dp.png",
      "useLocaleFromApp": true,
      "homepageTrigger": {
        "runFunction": "onHomepage",
        "enabled": true
      },
      "universalActions": [{
        "label": "Learn more about Cataas",
        "openLink": "https://cataas.com"
      }]
    },
    "gmail": {
      "contextualTriggers": [{
        "unconditional": {
        },
        "onTriggerFunction": "onGmailMessage"
      }],
      "composeTrigger": {
        "selectActions": [{
          "text": "Insert cat",
          "runFunction": "onGmailCompose"
        }],
        "draftAccess": "NONE"
      }
    },
    "drive": {
      "onItemsSelectedTrigger": {
        "runFunction": "onDriveItemsSelected"
      }
    },
    "calendar": {
      "eventOpenTrigger": {
        "runFunction": "onCalendarEventOpen"
      }
    }
  }
}
```

### Install a test deployment

1. In your Apps Script project, click **Editor**.
2. Click **Deploy** > **Test deployments**.
3. Click **Install** > **Done**.

## Run the script

1. Go to [Gmail](https://mail.google.com/).
2. In the right side panel, click Cats to open the add-on.
3. If prompted, authorize the add-on.
4. The add-on displays a cat image and text. To change the image, click **Change cat**.
5. If you open an email while the add-on is open, the image refreshes and the text changes to the subject line of the email (truncated if it's too long).

You can see similar functionality in Calendar and Drive. You don't need to reauthorize the add-on to use it in those host apps.

## Next steps

- [Extend Google Workspace with add-ons](https://developers.google.com/workspace/add-ons/overview)
- [Build Google Workspace add-ons](https://developers.google.com/workspace/add-ons/how-tos/building-workspace-addons)
- [Publish an app](https://developers.google.com/workspace/marketplace/how-to-publish)

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0).
