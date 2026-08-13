# Gmail Manifest Resource Documentation

## Gmail

The Google Workspace add-on manifest configuration for Gmail extensions.

**JSON representation:**
```json
{
  "authorizationCheckFunction": string,
  "composeTrigger": {
    object (ComposeTrigger)
  },
  "contextualTriggers": [
    {
      object (ContextualTrigger)
    }
  ],
  "homepageTrigger": {
    object (HomepageTrigger)
  }
}
```

**Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `authorizationCheckFunction` | string | **Deprecated.** The name of an Apps Script function performing third-party authorization checks. |
| `composeTrigger` | object (ComposeTrigger) | **Required for compose actions.** Defines the UIs available when composing an email. |
| `contextualTriggers[]` | object (ContextualTrigger) | **Required.** List of triggers that fire when a message opens in Gmail. Only one criteria available (`unconditional`); array limited to single trigger. |
| `homepageTrigger` | object (HomepageTrigger) | The trigger function for the add-on homepage in Gmail. Overrides `addOns.common.homepageTrigger`. |

---

## ComposeTrigger

Configuration for a compose action defining available UIs when composing email.

**JSON representation:**
```json
{
  "draftAccess": string,
  "selectActions": [
    {
      object (SelectAction)
    }
  ]
}
```

**Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `draftAccess` | string | Defines data access level for compose trigger function. Valid options: `NONE` (default) or `METADATA` (requires `gmail.addons.current.message.metadata` scope). |
| `selectActions[]` | object (SelectAction) | List of compose actions **limited to single action per add-on**. |

---

## ContextualTrigger

Configuration for triggers firing when users open Gmail messages.

**JSON representation:**
```json
{
  "onTriggerFunction": string,
  "unconditional": {}
}
```

**Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `onTriggerFunction` | string | **Required for each contextual trigger.** The name of the Apps Script function executed when the trigger fires. |
| `unconditional` | object | **Required for each contextual trigger.** Specifies trigger activation for all opened Gmail messages; should be empty object. |

---

## SelectAction

Compose action configuration defining the function executed when selected.

**JSON representation:**
```json
{
  "runFunction": string,
  "text": string
}
```

**Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `runFunction` | string | **Required for compose actions.** The name of the Apps Script function executed when selected. Builds the add-on compose UI. |
| `text` | string | **Required for compose actions.** A short description of the action. |

Source: https://developers.google.com/apps-script/manifest/gmail-addons
