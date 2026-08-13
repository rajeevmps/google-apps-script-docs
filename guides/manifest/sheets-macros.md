# Sheets macro manifest resource

## Page Summary

- To define Sheets macros, you must use a specific configuration within a manifest, ensuring all required fields are included.
- The top-level Sheets configuration in the manifest is exclusively used for defining Sheets macros and contains a required list of macro objects.
- Each individual Macro object within the manifest configuration requires defining a function name and a menu name.
- Macros can optionally have a unique default keyboard shortcut defined using the format "Ctrl+Alt+Shift+Number".

## Sheets

The top-level of the Sheets macro manifest configuration. This is only used to define Sheets macros.

### JSON representation

```json
{
  "macros": [
    {
      object (Macro)
    }
  ]
}
```

### Fields

| Field | Type | Description |
|-------|------|-------------|
| `macros[]` | object (Macro) | **Required.** A list of defined macros and their associated properties. |

## Macro

The configuration for a single macro. Definitions must include all fields marked as **Required**.

### JSON representation

```json
{
  "defaultShortcut": string,
  "functionName": string,
  "menuName": string
}
```

### Fields

| Field | Type | Description |
|-------|------|-------------|
| `defaultShortcut` | string | The keyboard shortcut that executes the macro. It must be in the form `Ctrl+Alt+Shift+*Number*`. Macros without shortcuts can only be executed from the **Tools** > **Macros** menu. The keyboard shortcut used by each defined macro must be unique. |
| `functionName` | string | **Required.** The name of the Apps Script function that executes the macro. By default, this matches the `menuName` for functions automatically created, but this is not a requirement. |
| `menuName` | string | **Required.** The name of the macro as it appears in the Google Sheets UI. |

Source: https://developers.google.com/apps-script/manifest/sheets
