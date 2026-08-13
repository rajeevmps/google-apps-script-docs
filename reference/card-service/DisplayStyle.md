# DisplayStyle

An enum that defines a style for displaying cards when they are pushed.

An enum that defines a style for displaying cards when they are pushed.

`DisplayStyle.REPLACE` shows the card by replacing the current view of the top card in the card stack. `DisplayStyle.PEEK` displays the card header at the bottom of the sidebar, partially covering the existing top card; clicking the header adds it to the stack. If no header exists, a generated one is used.

This enum only applies to cards returned from contextual trigger functions.

To call an enum, you call its parent class, name, and property. For example, `CardService.DisplayStyle.PEEK`.

## Properties

### PEEK
Show the card header at the bottom of add-on content over existing content.

### REPLACE
Show the card by replacing existing content.
