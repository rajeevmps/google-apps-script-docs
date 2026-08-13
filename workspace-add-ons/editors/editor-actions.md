# Editor actions

## Page Summary

- Google Workspace add-ons use Action objects to define interactive behavior triggered by user interactions with UI widgets.
- An action's callback function executes when triggered and receives an event object containing interaction details, requiring a specific response object to be returned.
- Add-ons extending Editors and using REST APIs can request file access using a widget action with a specialized response object returned by its callback function.
- Requesting file access involves building a homepage card to check for `drive.file` scope and providing a way for users to grant this scope if needed.

## Add an action to a widget

To attach an action to a widget, use a widget handler function, which also defines the condition that triggers the action. When triggered, the action executes a designated callback function. The callback function is passed an event object that carries information about the user's client-side interactions. You must implement the callback function and have it return a specific response object.

### Example: Display a new card when a button is clicked

If you want to add a button to your add-on that builds and displays a new card when clicked, follow these steps:

1. Create a button widget.
2. To set a card-building action, add the button widget handler function `setOnClickAction`.
3. Create an Apps Script callback function to execute and specify it as the `action` within the widget handler function. In this case, the callback function should build the card you want and return an `ActionResponse` object. The response object tells the add-on to display the card the callback function built.

The following example shows the creation of a button widget. The action requests the `drive.file` scope for the current file on behalf of the add-on.

```javascript
/**
     * Adds a section to the Card Builder that displays a "REQUEST PERMISSION"
     * button. When it's clicked, the callback triggers file scope permission flow.
     * This is used in the add-on when the home-page displays basic data.
     */
    function addRequestFileScopeButtonToBuilder(cardBuilder) {
        var buttonSection = CardService.newCardSection();
        // If the add-on does not have access permission, add a button that
        // lets the user provide that permission on a per-file basis.
        var buttonAction = CardService.newAction()
          .setFunctionName("onRequestFileScopeButtonClickedInEditor");
    
        var button = CardService.newTextButton()
          .setText("Request permission")
          .setBackgroundColor("#4285f4")
          .setTextButtonStyle(CardService.TextButtonStyle.FILLED)
          .setOnClickAction(buttonAction);
    
        buttonSection.addWidget(button);
        cardBuilder.addSection(buttonSection);
    }
    
    /**
     * Callback function for a button action. Instructs Docs to display a
     * permissions dialog to the user, requesting `drive.file` scope for the 
     * current file on behalf of this add-on.
     *
     * @param {Object} e The parameters object that contains the document's ID
     * @return {editorFileScopeActionResponse}
     */
    function onRequestFileScopeButtonClickedInEditor(e) {
      return CardService.newEditorFileScopeActionResponseBuilder()
          .requestFileScopeForActiveDocument().build();
    }
```

## File access interactions for REST APIs

Google Workspace add-ons that extend the Editors and use REST APIs can include an additional widget action to request file access. This action requires the associated action callback function to return a specialized response object:

| Action attempted | Callback function should return |
|---|---|
| Request file access | `EditorFileScopeActionResponse` |

To make use of this widget action and response object, all of the following must be true:

- The add-on uses REST APIs.
- The add-on presents the request file scope dialog using the `CardService.newEditorFileScopeActionResponseBuilder().requestFileScopeForActiveDocument().build();` method.
- The add-on includes the `https://www.googleapis.com/auth/drive.file` editor scope and `onFileScopeGranted` trigger in its manifest.

### Request file access for current document

To request file access for the current document, follow these steps:

1. Build a homepage card that checks whether the add-on has `drive.file` scope.
2. For cases where the add-on hasn't been granted `drive.file` scope, build a way to request that users grant `drive.file` scope for the current document.

#### Example: Get current document access in Docs

The following example builds an interface for Docs that displays the size of the current document. If the add-on doesn't have `drive.file` authorization, it displays a button to initiate the file scope authorization.

```javascript
/**
     * Build a card that checks selected items' quota usage. Checking
     * quota usage requires user-permissions, so this add-on provides a button
     * to request `drive.file` scope for items the add-on doesn't yet have
     * permission to access.
     *
     * @param e The event object passed containing information about the
     *   current document.
     * @return {Card}
     */
    function onDocsHomepage(e) {
      return createAddOnView(e);
    }
    
    function onFileScopeGranted(e) {
      return createAddOnView(e);
    }
    
    /**
     * For the current document, display either its quota information or
     * a button that lets the user provide permission to access that
     * file to retrieve its quota details.
     *
     * @param e The event containing information about the current document
     * @return {Card}
     */
    function createAddOnView(e) {
      var docsEventObject = e['docs'];
      var builder =  CardService.newCardBuilder();
    
      var cardSection = CardService.newCardSection();
      if (docsEventObject['addonHasFileScopePermission']) {
        cardSection.setHeader(docsEventObject['title']);
        // This add-on uses the recommended, limited-permission `drive.file`
        // scope to get granular per-file access permissions.
        // See: https://developers.google.com/drive/api/v2/about-auth
        // If the add-on has access permission, read and display its quota.
        cardSection.addWidget(
          CardService.newTextParagraph().setText(
              "This file takes up: " +
              getQuotaBytesUsed(docsEventObject['id'])));
      } else {
        // If the add-on does not have access permission, add a button that
        // lets the user provide that permission on a per-file basis.
        cardSection.addWidget(
          CardService.newTextParagraph().setText(
              "The add-on needs permission to access this file's quota."));
    
        var buttonAction = CardService.newAction()
          .setFunctionName("onRequestFileScopeButtonClicked");
    
        var button = CardService.newTextButton()
          .setText("Request permission")
          .setOnClickAction(buttonAction);
    
        cardSection.addWidget(button);
      }
      return builder.addSection(cardSection).build();
    }
    
    /**
     * Callback function for a button action. Instructs Docs to
     * display a permissions dialog to the user, requesting `drive.file` scope for
     * the current file on behalf of this add-on.
     *
     * @param {Object} e The parameters object that contains the document's ID
     * @return {editorFileScopeActionResponse}
     */
    function onRequestFileScopeButtonClicked(e) {
      return CardService.newEditorFileScopeActionResponseBuilder()
          .requestFileScopeForActiveDocument().build();
    }
```
