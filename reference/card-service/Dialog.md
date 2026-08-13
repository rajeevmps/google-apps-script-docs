# Dialog

A builder for Dialog objects.

A builder for `Dialog` objects. Only available for Google Chat apps. Not available for Google Workspace add-ons. Dialogs are only available for Google Chat apps, not Google Workspace add-ons.

## Methods

### setBody(card: Card): Dialog

Sets the card of the `Dialog`.

Parameters:
- `card` (Card): The `Card` to use.

Return: `Dialog` — This object, for chaining.

```javascript
const card = CardService.newCardBuilder()
                 .setHeader(CardService.newCardHeader().setTitle('Card title'))
                 .build();

// Sets the card of the dialog.
const dialog = CardService.newDialog().setBody(card);
```
