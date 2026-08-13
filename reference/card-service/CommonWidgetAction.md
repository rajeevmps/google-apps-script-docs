# CommonWidgetAction

Defines actions that don't involve evaluations, such as updating widget visibility.

Defines actions that don't involve evaluations, such as updating widget visibility. For example, can reveal or hide widgets based on the value of an input as part of CEL validation.

Only available for Google Workspace add-ons that extend Google Workspace Studio.

```javascript
const commonWidgetAction = CardService.newCommonWidgetAction()
.setUpdateVisibilityAction(CardService.Visibility.VISIBLE);
```

## Methods

### setUpdateVisibilityAction(updateVisibilityAction: UpdateVisibilityAction): CommonWidgetAction

Sets the update visibility action for widgets.

Parameters: `updateVisibilityAction` (UpdateVisibilityAction) — The update visibility action.

Returns: The CommonWidgetAction, for chaining.
