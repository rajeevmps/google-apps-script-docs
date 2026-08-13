# Suggestions

Autocomplete suggestions to supplement a TextInput widget.

Autocomplete suggestions to supplement a TextInput widget. Available for Google Workspace add-ons and Google Chat apps.

## Methods

### addSuggestion(suggestion: String): Suggestions

Add a text suggestion.

Parameters:
- `suggestion` (String): The suggestion text.

Return: This object, for chaining.

### addSuggestions(suggestions: Object[]): Suggestions

Add a list of text suggestions.

Parameters:
- `suggestions` (Object[]): An array of string suggestions.

Return: This object, for chaining.

```javascript
const textInput = CardService.newTextInput().setSuggestions(
    CardService.newSuggestions()
        .addSuggestion('First suggestion')
        .addSuggestion('Second suggestion'),
);
```
