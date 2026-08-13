# ExecutionError

Source: https://developers.google.com/apps-script/api/reference/rest/v1/ExecutionError

## Overview

The `ExecutionError` object provides details about errors that occur when executing a script function through the Apps Script API. When a `run` call succeeds but the script throws an exception, the response's `error` field contains a `Status` object whose `details` field includes an `ExecutionError`.

## JSON Representation

```json
{
  "scriptStackTraceElements": [
    {
      object (ScriptStackTraceElement)
    }
  ],
  "errorMessage": string,
  "errorType": string
}
```

## Fields

| Field | Type | Description |
|-------|------|-------------|
| `scriptStackTraceElements[]` | `ScriptStackTraceElement` | An array of objects showing the stack trace through the script, with the deepest call first, indicating where execution failed |
| `errorMessage` | `string` | The error message thrown by Apps Script, typically localized to the user's language |
| `errorType` | `string` | The error type (e.g., `TypeError`, `ReferenceError`). This field is not included if the error type is unavailable |

## ScriptStackTraceElement

Represents a single level in the stack trace showing where execution failed.

### JSON Representation

```json
{
  "function": string,
  "lineNumber": integer
}
```

### Fields

| Field | Type | Description |
|-------|------|-------------|
| `function` | `string` | The name of the function that failed |
| `lineNumber` | `integer` | The line number where the script failed |
</content>
