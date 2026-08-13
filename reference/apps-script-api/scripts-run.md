# Method: scripts.run

Source: https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run

## Overview

The `scripts.run` method executes a function within a deployed Apps Script project via the Apps Script API. It requires OAuth 2.0 authorization and the script project must be deployed as an API Executable.

## HTTP Request

```
POST https://script.googleapis.com/v1/scripts/{deploymentId}:run
```

## Path Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `deploymentId` | string | The deployment ID found under **Deploy > Manage deployments** in the script editor |

## Request Body

```json
{
  "function": string,
  "parameters": [value],
  "sessionState": string,
  "devMode": boolean
}
```

| Field | Type | Description |
|-------|------|-------------|
| `function` | string | Function name to execute (can reference library functions like `Library.libFunction1`) |
| `parameters[]` | value (protobuf Value) | Optional parameters passed to the function; must be primitive types (string, number, array, object, boolean) |
| `sessionState` | string | **Deprecated**. Android add-ons only; represents user session in Docs/Sheets app |
| `devMode` | boolean | If true and user owns script, runs latest saved version; default is false |

## Response Body

```json
{
  "done": boolean,
  "error": {Status object},
  "response": {object with @type field}
}
```

| Field | Type | Description |
|-------|------|-------------|
| `done` | boolean | Indicates whether execution completed |
| `error` | Status object | Present if script throws exception; contains ExecutionError details |
| `response` | object | Present on success; contains ExecutionResponse with result |

## Status Object (Error Response)

```json
{
  "code": integer,
  "message": string,
  "details": [{@type, fields...}]
}
```

| Field | Type | Values |
|-------|------|--------|
| `code` | integer | 10 (SCRIPT_TIMEOUT), 3 (INVALID_ARGUMENT), or 1 (CANCELLED) |
| `message` | string | English developer-facing error message |
| `details[]` | object | Array with single ExecutionError object |

## Authorization Scopes Required

The API requires at least one scope from this list:
- `https://www.googleapis.com/auth/script.scriptapp`
- `https://www.googleapis.com/auth/script.external_request`
- `https://www.googleapis.com/auth/script.send_mail`
- `https://www.googleapis.com/auth/script.storage`
- `https://www.googleapis.com/auth/documents`
- `https://www.googleapis.com/auth/spreadsheets`
- `https://www.googleapis.com/auth/drive`
- `https://www.googleapis.com/auth/forms`
- Plus 15 additional authorization scopes listed in the official documentation (varies by the APIs/services the script itself calls)

## Key Constraints

- Maximum execution runtime follows [Apps Script quotas](https://developers.google.com/apps-script/guides/services/quotas#current_limitations) (external — not scraped)
- Script project must share same Cloud Platform project as caller
- Parameters cannot be Apps Script-specific types (Document, Calendar, etc.)
- Error `403 PERMISSION_DENIED` indicates mismatched Cloud Platform projects
</content>
