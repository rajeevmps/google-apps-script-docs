# Interaction

An enum type that specifies what to do in response to an interaction with a user, such as a user clicking a button in a card message.

An enum type that specifies what to do in response to an interaction with a user, such as a user clicking a button in a card message.

Only available for Google Chat apps. Not available for Google Workspace add-ons.

To call an enum, you call its parent class, name, and property. For example, `CardService.Interaction.OPEN_DIALOG`.

## Properties

### INTERACTION_UNSPECIFIED
Default value. The `action` executes as normal.

### OPEN_DIALOG
Opens a dialog, a card-based interface that Chat apps use to interact with users.
