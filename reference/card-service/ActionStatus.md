# ActionStatus

The status for a request to either invoke or submit a dialog.

The `ActionStatus` class represents the status for a request to either invoke or submit a dialog. It is only available for Google Chat apps and not for Google Workspace add-ons.

## Methods

### setStatusCode(statusCode: Status): ActionStatus

Represents the status for a request to either open or submit a dialog.

Parameters:
- `statusCode` (Status): The status code.

Returns: This object, for chaining.

```javascript
const actionStatus = CardService.newActionStatus().setStatusCode(
    CardService.Status.OK,
);
```

### setUserFacingMessage(message: String): ActionStatus

The message to send users about the status of their request. If unset, a generic message based on the `Status` is sent.

Parameters:
- `message` (String): The message to send.

Returns: This object, for chaining.

```javascript
const actionStatus =
    CardService.newActionStatus().setUserFacingMessage('Success');
```
