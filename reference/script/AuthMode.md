# AuthMode

An enumeration that identifies which categories of authorized services Apps Script is able to execute through a triggered function.

An enumeration that identifies which categories of authorized services Apps Script is able to execute through a triggered function. These values are exposed in triggered functions as the `authMode` property of the event parameter, `e`.

## Properties

### NONE

A mode that does not allow access to any services that require authorization. This mode occurs when an add-on executes an `onOpen(e)` simple trigger, and the user has installed an add-on in a different document but the add-on has not been used in the current document.

### CUSTOM_FUNCTION

A mode that allows access to a limited subset of services for use in custom spreadsheet functions. Some of these services — including read-only access to Spreadsheet service — normally require authorization, but are permitted without authorization when used in a custom function. Because custom functions do not include an event parameter, this value is never returned; it is documented only to demonstrate that custom functions run in their own authorization mode.

### LIMITED

A mode that allows access to a limited subset of services. This mode occurs when an add-on or a script bound to a document executes an `onOpen(e)` or `onEdit(e)` simple trigger, except in the case described for `NONE`.

### FULL

A mode that allows access to all services that require authorization. This mode occurs when an add-on or a script executes as the result of any trigger other than the cases described for `LIMITED` or `NONE`.
