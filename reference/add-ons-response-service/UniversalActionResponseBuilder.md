# UniversalActionResponseBuilder

A builder for `UniversalActionResponse` objects.

A builder for the `UniversalActionResponse` objects.

## Methods

### build()

`build(): UniversalActionResponse`

Builds the current universal action response and validates it.

**Returns**
- `UniversalActionResponse` — A validated UniversalActionResponse.

**Throws:** Error if the constructed universal action response isn't valid.

### displayAddOnCards(cardObjects)

`displayAddOnCards(cardObjects: Object[]): UniversalActionResponseBuilder`

Displays the add-on with the specified cards.

**Parameters**
- `cardObjects` (Object[]) — An array of `Card`s to display.

**Returns**
- `UniversalActionResponseBuilder` — This object, for chaining.

### setOpenLink(openLink)

`setOpenLink(openLink: OpenLink): UniversalActionResponseBuilder`

Sets the URL to open when the universal action is selected.

**Parameters**
- `openLink` (OpenLink) — The link object to use.

**Returns**
- `UniversalActionResponseBuilder` — This object, for chaining.
