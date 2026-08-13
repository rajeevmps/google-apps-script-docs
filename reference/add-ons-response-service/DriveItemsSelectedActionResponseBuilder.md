# DriveItemsSelectedActionResponseBuilder

A builder for `DriveItemsSelectedActionResponse` objects.

A builder for `DriveItemsSelectedActionResponse` objects.

## Methods

### build()

`build(): DriveItemsSelectedActionResponse`

Builds the current Drive action response.

**Returns**
- `DriveItemsSelectedActionResponse` — A validated `DriveItemsSelectedActionResponse`.

### requestFileScope(itemId)

`requestFileScope(itemId: String): DriveItemsSelectedActionResponseBuilder`

Specifies that the response requests file scope for the contextually-relevant item in Drive.

**Parameters**
- `itemId` (String) — ID of the Drive item to request file scope for.

**Returns**
- `DriveItemsSelectedActionResponseBuilder` — This object, for chaining.
