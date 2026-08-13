# ConferenceErrorType

Enum that defines the types of errors that you can specify in a ConferenceError.

Enum that defines the types of errors that you can specify in a `ConferenceError`. Access properties by calling the parent class, name, and property—for example, `ConferenceDataService.ConferenceErrorType.AUTHENTICATION`.

## Properties (Enum Values)

| Property | Description |
|----------|--------------|
| `AUTHENTICATION` | An authentication error during conference data generation. |
| `CONFERENCE_SOLUTION_FORBIDDEN` | The user is not allowed to use the selected conference solution (but might be allowed to use other solutions offered by the add-on). |
| `PERMANENT` | A permanent error during conference data generation. |
| `PERMISSION_DENIED` | The user isn't allowed to perform an action in the third-party conferencing system. |
| `TEMPORARY` | A temporary error during conference data generation. |
| `UNKNOWN` | An unknown error during conference data generation. |
