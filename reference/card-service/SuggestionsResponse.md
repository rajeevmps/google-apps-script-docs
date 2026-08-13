# SuggestionsResponse

A response object that can be returned from a suggestions callback function.

A response object that can be returned from a suggestions callback function. This is used with `TextInput` widgets that implement autocomplete.

Available for Google Workspace add-ons and Google Chat apps.

## Methods

### printJson(): String

Prints the JSON representation of this object. This is for debugging only.

```javascript
const suggestionsResponse = CardService.newSuggestionsResponseBuilder()
                                .setSuggestions(
                                    CardService.newSuggestions()
                                        .addSuggestion('First suggestion')
                                        .addSuggestion('Second suggestion'),
                                    )
                                .build();
```
