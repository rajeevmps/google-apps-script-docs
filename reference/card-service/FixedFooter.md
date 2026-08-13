# FixedFooter

A FixedFooter is a component shown at the bottom of a Card, available for Google Workspace add-ons and Google Chat apps.

The implementation supports a primary button, which must be a filled text button, and optionally a secondary button, which must be an outlined text button and is only shown if a primary button is set.

## Methods

### setPrimaryButton(button: TextButton): FixedFooter

Set the primary button in the fixed footer. The primary button must be a TextButtonStyle.FILLED button. If the background color is unset for the primary button, the button uses the primary color defined in the add-on manifest.

Parameters:
- `button` (TextButton) - The button to add.

Returns: This object, for chaining.

### setSecondaryButton(button: TextButton): FixedFooter

Set the secondary button in the fixed footer. The secondary button must be a TextButtonStyle.OUTLINED button. This method does nothing if setPrimaryButton(button) isn't called to set the primary button.

Parameters:
- `button` (TextButton) - The button to add.

Returns: This object, for chaining.

```javascript
const fixedFooter = CardService.newFixedFooter().setPrimaryButton(
    CardService.newTextButton().setText('help').setOpenLink(
        CardService.newOpenLink().setUrl('http://www.google.com')),
);
```
