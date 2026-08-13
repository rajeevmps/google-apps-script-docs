# Autocomplete suggestions for text inputs

The [Text Input](/apps-script/reference/card-service/text-input) widget lets your add-on read and react to text that users provide. You can configure these widgets to provide users automatic suggestions for input text.

Suggestions can come from a static list of strings. Alternatively, you can build suggestions from context, such as the text the user typed into the widget.

## Configure suggestions

To configure suggestions for a text input, follow these steps:

*   Create a list of suggestions by:
    *   Creating a static list.
    *   Defining an [action](/workspace/add-ons/concepts/actions) with a callback function that builds that list dynamically from context. You can use either method, or both.
*   Attach the suggestions list or action to the text input widget.

If you provide both a static list of suggestions and an action, the application uses the static list until the user starts entering characters. Then, the application uses the callback function and ignores the static list.

### Static suggestions

To offer a static list of suggestions, follow these steps:

1.  Create a [`Suggestions`](/apps-script/reference/card-service/suggestions) object.
2.  Add each static suggestion to it using [`addSuggestion`](/apps-script/reference/card-service/suggestions#addSuggestion\(String\)) or [`addSuggestions`](/apps-script/reference/card-service/suggestions#addsuggestionssuggestions).
3.  Attach the [`Suggestions`](/apps-script/reference/card-service/suggestions) object to the widget using [`TextInput.setSuggestions`](/apps-script/reference/card-service/text-input#setsuggestionssuggestions).

The application displays static suggestions in the order that they're added. It also automatically performs case-insensitive prefix matching and filters the suggestion list as the user types.

### Suggestion actions

If you don't use a static suggestion list, define an action to build suggestions dynamically. Follow these steps:

1.  Create an [`Action`](/apps-script/reference/card-service/action) object and associate it with a [callback function](/workspace/add-ons/concepts/actions#callback_functions) you define.
2.  Call the widget's [`TextInput.setSuggestionsAction`](/apps-script/reference/card-service/text-input#setsuggestionsactionsuggestionsaction) function, providing it the [`Action`](/apps-script/reference/card-service/action) object.
3.  Implement the callback function to build the suggestion list and return a built [`SuggestionsResponse`](/apps-script/reference/card-service/suggestions-response) object.

The application calls the callback function whenever the user types a character, but only after the user stops typing for a moment. The callback function receives an _event object_ with information about the open card's widgets. See [Action event objects](/workspace/add-ons/concepts/actions#action_event_objects).

The callback function must return a [`SuggestionsResponse`](/apps-script/reference/card-service/suggestions-response) with the list of suggestions to display. The application displays suggestions in the order that they're added. Unlike static lists, the application doesn't automatically filter callback suggestions based on user input. To filter, read the text input value from the event object and filter suggestions as you construct the list.

### Example

The following snippet shows how to configure suggestions on two different text input widgets: the first with a static list and the second with a callback function.

```
// Create an input with a static suggestion list.
    var textInput1 = CardService.newTextInput()
        .setFieldName('colorInput')
        .setTitle('Color choice')
        .setSuggestions(CardService.newSuggestions()
            .addSuggestion('Red')
            .addSuggestion('Yellow')
            .addSuggestions(['Blue', 'Black', 'Green']));
    
    // Create an input with a dynamic suggestion list.
    var action = CardService.newAction()
        .setFunctionName('refreshSuggestions');
    var textInput2 = CardService.newTextInput()
        .setFieldName('emailInput')
        .setTitle('Email')
        .setSuggestionsAction(action);
    
    // ...
    
    /**
     *  Build and return a suggestion response. In this case, the suggestions
     *  are a list of emails taken from the To: and CC: lists of the open
     *  message in Gmail, filtered by the text that the user has already
     *  entered. This method assumes the Google Workspace
     *  add-on extends Gmail; the add-on only calls this method for cards
     *  displayed when the user has entered a message context.
     *
     *  @param {Object} e the event object containing data associated with
     *      this text input widget.
     *  @return {SuggestionsResponse}
     */
     function refreshSuggestions(e) {
       // Activate temporary Gmail scopes, in this case so that the
       // open message metadata can be read.
       var accessToken = e.gmail.accessToken;
       GmailApp.setCurrentMessageAccessToken(accessToken);
    
       var userInput = e && e.formInput['emailInput'].toLowerCase();
       var messageId = e.gmail.messageId;
       var message = GmailApp.getMessageById(messageId);
    
       // Combine the comma-separated returned by these methods.
       var addresses = message.getTo() + ',' + message.getCc();
    
       // Filter the address list to those containing the text the user
       // has already entered.
       var suggestionList = [];
       addresses.split(',').forEach(function(email) {
         if (email.toLowerCase().indexOf(userInput) !== -1) {
           suggestionList.push(email);
         }
       });
       suggestionList.sort();
    
       return CardService.newSuggestionsResponseBuilder()
           .setSuggestions(CardService.newSuggestions()
               .addSuggestions(suggestionList))
           .build();  // Don't forget to build the response!
     }
```

## Suggestions and `setOnChangeAction`

Text input widgets can have a [`setOnChangeAction`](/workspace/add-ons/concepts/actions#setOnChangeAction) handler function defined that executes whenever the widget loses focus. If both the handler and suggestions are enabled for the same text input, these rules define the interaction behavior:

1.  The `setOnChangeAction` handler executes after a suggestion is selected.
2.  If the user presses Enter (or otherwise makes the text input lose focus) without modifying the selected suggestion, `setOnChangeAction` doesn't trigger again.
3.  `setOnChangeAction` does trigger again if the user, after selecting a suggestion, edits it so that it no longer matches any of the suggestions in the list.
4.  If the user doesn't select a suggestion, `setOnChangeAction` triggers when the text input loses focus.
