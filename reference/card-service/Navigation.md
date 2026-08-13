# Navigation

A helper object that controls card navigation. See the card navigation guide for more details.

## Methods

### popCard(): Navigation

Pops a card from the navigation stack. Can be chained with other card navigation actions.

### popToNamedCard(cardName: String): Navigation

Pops to the specified card by its card name. Can be chained with other card navigation actions.

Parameters:
- `cardName` (String) - The name of the card to navigate to.

### popToRoot(): Navigation

Pops the card stack to the root card. Can be chained with other card navigation actions.

### printJson(): String

Prints the JSON representation of this object. This is for debugging only.

### pushCard(card: Card): Navigation

Pushes the given card onto the stack. Can be chained with other card navigation actions.

Parameters:
- `card` (Card) - A card to add to the stack.

### updateCard(card: Card): Navigation

Does an in-place replacement of the current card. Can be chained with other card navigation actions.

Parameters:
- `card` (Card) - A card to replace the current card with.
