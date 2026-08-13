# REST Resource: processes

Source: https://developers.google.com/apps-script/api/reference/rest/v1/processes

## Resource Description

A Process resource represents a single script execution started from various sources like the script editor, triggers, or the Apps Script API. Unlike the Operation resource, Process specifically covers executions not solely initiated via the Apps Script API.

## JSON Representation

```json
{
  "projectName": string,
  "functionName": string,
  "processType": enum (ProcessType),
  "processStatus": enum (ProcessStatus),
  "userAccessLevel": enum (UserAccessLevel),
  "startTime": string,
  "duration": string
}
```

## Fields

| Field | Type | Description |
|-------|------|-------------|
| `projectName` | string | Name of the script being executed |
| `functionName` | string | Name of the function that started the execution |
| `processType` | enum (ProcessType) | The execution type |
| `processStatus` | enum (ProcessStatus) | The execution status |
| `userAccessLevel` | enum (UserAccessLevel) | The executing user's access level to the script |
| `startTime` | string (Timestamp) | Time the execution started in RFC3339 UTC format |
| `duration` | string (Duration) | Duration the execution spent executing in seconds with up to nine fractional digits |

## ProcessType Enum

| Value | Description |
|-------|-------------|
| `PROCESS_TYPE_UNSPECIFIED` | Unspecified type |
| `ADD_ON` | Started from an add-on entry point |
| `EXECUTION_API` | Started using the Apps Script API |
| `TIME_DRIVEN` | Started from a time-based trigger |
| `TRIGGER` | Started from an event-based trigger |
| `WEBAPP` | Started from a web app entry point |
| `EDITOR` | Started using the Apps Script IDE |
| `SIMPLE_TRIGGER` | Started from a G Suite simple trigger |
| `MENU` | Started from a G Suite menu item |
| `BATCH_TASK` | Started as a task in a batch job |

## ProcessStatus Enum

| Value | Description |
|-------|-------------|
| `PROCESS_STATUS_UNSPECIFIED` | Unspecified status |
| `RUNNING` | Currently running |
| `PAUSED` | Process has paused |
| `COMPLETED` | Process has completed |
| `CANCELED` | Process was cancelled |
| `FAILED` | Process failed |
| `TIMED_OUT` | Process timed out |
| `UNKNOWN` | Status unknown |
| `DELAYED` | Waiting for quota |

## UserAccessLevel Enum

| Value | Description |
|-------|-------------|
| `USER_ACCESS_LEVEL_UNSPECIFIED` | Unspecified |
| `NONE` | No access |
| `READ` | Read-only access |
| `WRITE` | Write access |
| `OWNER` | Owner access |

## Methods

### list
GET `/v1/processes` — Retrieve information about processes made by or on behalf of a user, such as process type and current status.

### listScriptProcesses
GET `/v1/processes:listScriptProcesses` — Retrieve information about a script's executed processes, such as process type and current status.
</content>
