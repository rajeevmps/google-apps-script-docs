# Universal actions

Universal actions are menu items that let you open a web page, display UI cards, or run an Apps Script function. They're similar to card actions, but universal actions appear on every card in the add-on, regardless of context.

Use universal actions to ensure that users always have access to certain functionality. Example uses for universal actions include:

*   Open a settings web page or display a settings card.
*   Show help information.
*   Start a new workflow, such as 'Add new customer'.
*   Display a card to send feedback about the add-on.

If an action doesn't depend on the current context, consider making it a universal action.

## Use universal actions

Configure universal actions in the add-on's manifest. After you configure a universal action, it's always available to users. If a user views a card, the universal actions appear in the card menu (more_vert) after any card actions. Universal actions appear in the menu in the order they're defined in the manifest.

## Configure universal actions

Configure universal actions in the add-on's manifest. See Manifests.

For each action, specify the text that appears in the menu. You can specify an `openLink` field to open a web page in a new tab. Alternatively, specify a `runFunction` field to call an Apps Script callback function when the user selects the action.

When you use `runFunction`, the callback function usually does one of the following:

*   Builds UI cards to display immediately by returning a `UniversalActionResponse` object.
*   Opens a URL, perhaps after other tasks, by returning a `UniversalActionResponse` object.
*   Conducts background tasks that don't switch cards or open a URL. In this case, the callback function returns nothing.

The application passes the callback function an event object with information about the open card and add-on context.

**Warning:** To keep the add-on responsive, the Card service limits universal action callback functions to 30 seconds of execution time. If execution takes longer, the UI might not update properly.

## Example

The following snippet shows an example manifest excerpt for an add-on that uses universal actions while extending Gmail. The code sets a metadata scope so that the add-on can determine who sent the open message.

```
"oauthScopes": [
      "https://www.googleapis.com/auth/gmail.addons.current.message.metadata"
    ],
    "addOns": {
      "common": {
        "name": "Universal Actions Only Addon",
        "logoUrl": "https://www.example.com/hosted/images/2x/my-icon.png",
        "openLinkUrlPrefixes": [
          "https://www.google.com",
          "https://www.example.com/urlbase"
        ],
        "universalActions": [{
            "label": "Open google.com",
            "openLink": "https://www.google.com"
          }, {
            "label": "Open contact URL",
            "runFunction": "openContactURL"
          }, {
            "label": "Open settings",
            "runFunction": "createSettingsResponse"
          }, {
            "label": "Run background sync",
            "runFunction": "runBackgroundSync"
        }],
        ...
      },
      "gmail": {
        "contextualTriggers": [
          {
            "unconditional": {},
            "onTriggerFunction": "getContextualAddOn"
          }
        ]
      },
      ...
    },
    ...
```

The universal actions in the example do the following:

*   **Open google.com** opens google.com in a new tab.
*   **Open contact URL** runs a function that determines which URL to open and opens it in a new tab using an `OpenLink` object. The code builds the URL using the sender's email address.
*   **Open settings** runs the `createSettingsCards` function. This function returns a `UniversalActionResponse` with cards for settings and other information. The UI displays the list of cards. See Return multiple cards.
*   **Run background sync** runs the `runBackgroundSync` function. This function doesn't build cards; instead, it performs background tasks. Because the function doesn't return a `UniversalActionResponse`, the UI doesn't display a new card. Instead, the UI displays a loading indicator while the function runs.

Here is an example of how you might construct the `openContactURL`, `createSettingsResponse`, and `runBackgroundSync` functions:

```
/**
     * Open a contact URL.
     * @param {Object} e an event object
     * @return {UniversalActionResponse}
     */
    function openContactURL(e) {
      // Activate temporary Gmail scopes, in this case so that the
      // open message metadata can be read.
      var accessToken = e.gmail.accessToken;
      GmailApp.setCurrentMessageAccessToken(accessToken);
    
      // Build URL to open based on a base URL and the sender's email.
      // This URL must be included in the openLinkUrlPrefixes whitelist.
      var messageId = e.gmail.messageId;
      var message = GmailApp.getMessageById(messageId);
      var sender = message.getFrom();
      var url = "https://www.example.com/urlbase/" + sender;
      return CardService.newUniversalActionResponseBuilder()
          .setOpenLink(CardService.newOpenLink()
              .setUrl(url))
          .build();
    }
    
    /**
     * Create a collection of cards to control the add-on
     * settings and present other information. These cards are displayed in a list
     * when the user selects the associated "Open settings" universal action.
     *
     * @param {Object} e an event object
     * @return {UniversalActionResponse}
     */
    function createSettingsResponse(e) {
      return CardService.newUniversalActionResponseBuilder()
          .displayAddOnCards(
              [createSettingCard(), createAboutCard()])
          .build();
    }
    
    /**
     * Create and return a built settings card.
     * @return {Card}
     */
    function createSettingCard() {
      return CardService.newCardBuilder()
          .setHeader(CardService.newCardHeader().setTitle('Settings'))
          .addSection(CardService.newCardSection()
              .addWidget(CardService.newSelectionInput()
                  .setType(CardService.SelectionInputType.CHECK_BOX)
                  .addItem("Ask before deleting contact", "contact", false)
                  .addItem("Ask before deleting cache", "cache", false)
                  .addItem("Preserve contact ID after deletion", "contactId", false))
              // ... continue adding widgets or other sections here ...
          ).build();   // Don't forget to build the card!
    }
    
    /**
     * Create and return a built 'About' informational card.
     * @return {Card}
     */
    function createAboutCard() {
      return CardService.newCardBuilder()
          .setHeader(CardService.newCardHeader().setTitle('About'))
          .addSection(CardService.newCardSection()
              .addWidget(CardService.newTextParagraph()
                  .setText('This add-on manages contact information. For more '
                      + 'details see the <a href="https://www.example.com/help">help page</a>.'))
          // ... add other information widgets or sections here ...
          ).build();  // Don't forget to build the card!
    }
    
    /**
     * Run background tasks, none of which should alter the UI.
     * Also records the time of sync in the script properties.
     *
     * @param {Object} e an event object
     */
    function runBackgroundSync(e) {
      var props = PropertiesService.getUserProperties();
      props.setProperty("syncTime", new Date().toString());
    
      syncWithContacts();  // Not shown.
      updateCache();       // Not shown.
      validate();          // Not shown.
    
      // no return value tells the UI to keep showing the current card.
    }
```
