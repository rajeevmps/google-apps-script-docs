# UpdateVisibilityAction

Updates the visibility of a card widget to make it display or to hide it.

Updates the visibility of a card widget to make it display or to hide it. Only available for Google Workspace add-ons that extend Google Workspace Studio.

```javascript
const updateVisibilityAction = CardService.newUpdateVisibilityAction()
.setVisibility(CardService.Visibility.VISIBLE);
```

## Methods

### setVisibility(visibility: Visibility): UpdateVisibilityAction

Sets the visibility of widgets to visible or hidden.

Parameters:
- `visibility` (Visibility): The visibility of the widgets.

Returns: The UpdateVisibilityAction, for chaining.
