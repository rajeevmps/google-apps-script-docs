# CardBuilder

A builder for Card objects.

CardBuilder is used to build Card objects. You can add card actions and sections to a Card using the builder. The `build()` method finalizes and validates the Card object. Various methods allow setting the card's display style, footer, header, name, and peek card header.

## Methods

### addCardAction(cardAction: CardAction): CardBuilder

Adds a CardAction to this Card.

Parameters:
- `cardAction` (CardAction): The CardAction to use.

Returns: This object, for chaining.

### addExpressionData(expressionData: ExpressionData): CardBuilder

Adds an expression data to this card. The ExpressionData defines the CEL logic and condition as well as what event to trigger when a condition is satisfied.

Parameters:
- `expressionData` (ExpressionData): The ExpressionData to use.

Returns: This object, for chaining.

### addSection(section: CardSection): CardBuilder

Adds a section to this card. You can't add more than 100 sections to a card.

Parameters:
- `section` (CardSection): The CardSection to use.

Returns: This object, for chaining.

### build(): Card

Builds the current card and validates it.

Returns: A validated card.

Throws: Error if the constructed card isn't valid.

### setDisplayStyle(displayStyle: DisplayStyle): CardBuilder

Sets the display style for this card. If set to REPLACE, the card replaces the top card view. If set to PEEK, the header appears at sidebar bottom, partially covering the current top card. Clicking the header pops the card into the stack. DisplayStyle only works for cards returned from contextual trigger functions.

Parameters:
- `displayStyle` (DisplayStyle): The DisplayStyle to set.

Returns: This object, for chaining.

### setFixedFooter(fixedFooter: FixedFooter): CardBuilder

Sets a fixed footer for this card.

Parameters:
- `fixedFooter` (FixedFooter): The FixedFooter to use.

Returns: This object, for chaining.

### setHeader(cardHeader: CardHeader): CardBuilder

Sets the header for this card.

Parameters:
- `cardHeader` (CardHeader): The CardHeader to use.

Returns: This object, for chaining.

### setName(name: String): CardBuilder

Sets the name for this card. The name can be used for navigation.

Parameters:
- `name` (String): The name.

Returns: This object, for chaining.

### setPeekCardHeader(peekCardHeader: CardHeader): CardBuilder

Sets the peek card header. The peek card is set on the first card returned from a contextual trigger function. It is used as a descriptive placeholder widget so that users can navigate from a homepage stack to the contextual stack.

Parameters:
- `peekCardHeader` (CardHeader): The CardHeader to set.

Returns: This object, for chaining.
