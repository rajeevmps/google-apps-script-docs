# DriveItemsSelectedActionResponseBuilder

A builder for DriveItemsSelectedActionResponse objects.

A builder for `DriveItemsSelectedActionResponse` objects. The `DriveItemsSelectedActionResponseBuilder` is used to create `DriveItemsSelectedActionResponse` objects. The `build()` method finalizes and returns the Drive action response object. The `requestFileScope(itemId)` method allows the response to request file scope for a specific Drive item.

## Methods

### build(): DriveItemsSelectedActionResponse

Builds the current Drive action response.

Return: A validated `DriveItemsSelectedActionResponse`.

### requestFileScope(itemId: String): DriveItemsSelectedActionResponseBuilder

Specifies that the response requests file scope for the contextually-relevant item in Drive.

Parameters:
- `itemId` (String): ID of the Drive item to request file scope for.

Return: This object, for chaining.
