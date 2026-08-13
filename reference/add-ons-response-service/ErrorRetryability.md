# ErrorRetryability

Represents the retry-ability of action invocation when having an error.

A Enum that represents the retry-ability of action invocation when having an error.

## Properties

| Property | Description |
|----------|-------------|
| `RETRYABILITY_UNSPECIFIED` | Unspecified. |
| `NOT_RETRYABLE` | The error is not retryable, the flow terminates after the first try. |
| `RETRYABLE` | The error is retryable, Workflow is going to try to execute the Step for up to 5 times. |
