# DialogAction

A builder for DialogAction objects.

DialogAction is a builder for DialogAction objects and is only available for Google Chat apps, not Google Workspace add-ons.

## Methods

### setActionStatus(actionStatus: ActionStatus): DialogAction

Sets the action status of `DialogAction`.

Return: This object, for chaining.

```javascript
const actionStatus = CardService.newActionStatus().setStatusCode(
    CardService.Status.OK,
);

const dialogAction =
    CardService.newDialogAction().setActionStatus(actionStatus);
```

### setDialog(dialog: Dialog): DialogAction

Sets the dialog of the `DialogAction`.

Return: This object, for chaining.

```javascript
const card = CardService.newCardBuilder()
                 .setHeader(CardService.newCardHeader().setTitle('card title'))
                 .build();

// Sets the card of the dialog.
const dialog = CardService.newDialog().setBody(card);

const dialogAction = CardService.newDialogAction().setDialog(dialog);
```
