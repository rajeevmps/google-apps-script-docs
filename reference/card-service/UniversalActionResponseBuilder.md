# UniversalActionResponseBuilder

A builder for UniversalActionResponse objects.

UniversalActionResponseBuilder is a builder for `UniversalActionResponse` objects. This class enables developers to construct universal action responses in Google Apps Script.

## Methods

### build(): UniversalActionResponse

Builds the current universal action response and validates it.

Returns: A validated UniversalActionResponse.

Throws: Error if the constructed universal action response isn't valid.

### displayAddOnCards(cardObjects: Object[]): UniversalActionResponseBuilder

Displays the add-on with the specified cards.

Parameters:
- `cardObjects` (Object[]): An array of Cards to display.

Returns: This object, for chaining.

### setOpenLink(openLink: OpenLink): UniversalActionResponseBuilder

Sets the URL to open when the universal action is selected.

Parameters:
- `openLink` (OpenLink): The link object to use.

Returns: This object, for chaining.
