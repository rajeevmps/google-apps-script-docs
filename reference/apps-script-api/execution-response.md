# ExecutionResponse

Source: https://developers.google.com/apps-script/api/reference/rest/v1/ExecutionResponse

## Overview

ExecutionResponse represents the return value of a function executed using the Apps Script API. When a script function executes successfully via the API, the response body's `response` field contains this object.

## Key Points

- **Return Value Format**: The `result` field holds the script function's return value as a `Value` object
- **Type Limitations**: "Functions called using the Apps Script API cannot return Apps Script-specific objects (such as a `Document` or a `Calendar`); they can only return primitive types"
- **Supported Types**: String, number, array, object, or boolean

## JSON Representation

```json
{
  "result": value
}
```

## Fields

| Field | Type | Description |
|-------|------|-------------|
| `result` | `Value` format | The return value of the script function. The type matches the object type returned in Apps Script. Only primitive types are supported. |

---

Content licensed under [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/); code samples under [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0).
</content>
