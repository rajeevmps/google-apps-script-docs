# SuggestionsResponseBuilder

A builder for SuggestionsResponse objects.

A builder for `SuggestionsResponse` objects. Available for Google Workspace add-ons and Google Chat apps.

## Methods

### build(): SuggestionsResponse

Builds the current suggestions response and validates it.

Return: `SuggestionsResponse` — A validated SuggestionsResponse.

Throws: `Error` if the constructed suggestions response isn't valid.

### setSuggestions(suggestions: Suggestions): SuggestionsResponseBuilder

Sets the suggestions used in auto complete in text fields.

Parameters:
- `suggestions` (Suggestions): The `Suggestions` to use.

Return: `SuggestionsResponseBuilder` — This object.
