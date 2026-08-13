# DataExecutionStatus

Access the status of a data execution.

The `DataExecutionStatus` object provides information about the status of a data execution. It includes methods to retrieve the error code, error message, execution state, last execution time, and last refreshed time. You can also check if the data from the last successful execution was truncated using the `isTruncated()` method.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `getErrorCode()` | `DataExecutionErrorCode` | Gets the error code of the data execution. |
| `getErrorMessage()` | `String` | Gets the error message of the data execution. The message may be empty. |
| `getExecutionState()` | `DataExecutionState` | Gets the state of the data execution. |
| `getLastExecutionTime()` | `Date\|null` | Gets the time the last data execution completed regardless of the execution state. Returns the last execution time, or `null` if there has never been a data execution. |
| `getLastRefreshedTime()` | `Date\|null` | Gets the time the data last successfully refreshed. Returns the last successfully refreshed time, or `null` if there is never a successful data execution. |
| `isTruncated()` | `Boolean` | Returns `true` if the data from last successful execution is truncated, or `false` otherwise. |
