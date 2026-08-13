# Calendar Manifest Resource Documentation

## Calendar

Configuration for Google Workspace add-on content and behavior within Google Calendar. All required components must be included if extending Calendar.

**JSON representation**

```json
{
  "createSettingsUrlFunction": string,
  "conferenceSolution": [
    {
      object (ConferenceSolution)
    }
  ],
  "currentEventAccess": string,
  "eventOpenTrigger": {
    object (EventOpenTrigger)
  },
  "eventUpdateTrigger": {
    object (EventUpdateTrigger)
  },
  "eventAttachmentTrigger": {
    object (EventAttachmentTrigger)
  },
  "homepageTrigger": {
    object (HomepageTrigger)
  }
}
```

**Fields**

| Field | Type | Description |
|-------|------|-------------|
| `createSettingsUrlFunction` | string | Optional. The Apps Script function name generating a URL to the add-on settings page. Only used for conferencing solutions. |
| `conferenceSolution[]` | object (ConferenceSolution) | Conferencing solutions offered by the add-on. Required if providing conferencing; at least one solution must be defined. |
| `currentEventAccess` | string | Determines add-on access level to event data: METADATA, READ, WRITE, or READ_WRITE. If omitted, no event metadata is passed. |
| `eventOpenTrigger` | object (EventOpenTrigger) | Trigger specification for when users open Calendar events. |
| `eventUpdateTrigger` | object (EventUpdateTrigger) | Required for contextual event update interfaces. Trigger specification for edited event saves. |
| `eventAttachmentTrigger` | object (EventAttachmentTrigger) | Trigger specification for attachment provider selection in Calendar menu. |
| `homepageTrigger` | object (HomepageTrigger) | The trigger function for the add-on homepage in Calendar, overriding common homepage settings. |

## ConferenceSolution

Configuration for third-party conferencing solutions offered by the add-on, appearing as options in Google Calendar's event editing interface.

**JSON representation**

```json
{
  "id": string,
  "logoUrl": string,
  "name": string,
  "onCreateFunction": string
}
```

**Fields**

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Required. Unique identifier for the conferencing solution. Do not change once chosen. |
| `logoUrl` | string | Link to solution icon (96 x 96 dp). Must be hosted on Google infrastructure. Differs from `calendar.logoUrl` if specified. |
| `name` | string | Required. Conferencing solution name displayed in Google Calendar UI. |
| `onCreateFunction` | string | Required. Apps Script function name called when Calendar attempts to create this conference type. |

## EventOpenTrigger

Configuration for contextual triggers firing when users open Google Calendar events.

**JSON representation**

```json
{
  "runFunction": string
}
```

**Fields**

| Field | Type | Description |
|-------|------|-------------|
| `runFunction` | string | Apps Script function name executing when a user opens a Calendar event. Must return array of Card objects. |

## EventUpdateTrigger

Configuration for contextual triggers firing when users edit and save Google Calendar events.

**JSON representation**

```json
{
  "runFunction": string
}
```

**Fields**

| Field | Type | Description |
|-------|------|-------------|
| `runFunction` | string | Apps Script function name executing when user saves an edited Calendar event. Must return array of Card objects. |

## EventAttachmentTrigger

Configuration for contextual triggers firing when users select the add-on attachment provider in the Calendar menu.

**JSON representation**

```json
{
  "runFunction": string,
  "label": string
}
```

**Fields**

| Field | Type | Description |
|-------|------|-------------|
| `runFunction` | string | Required. Apps Script function name executing upon provider selection. Must return array of Card objects. |
| `label` | string | Required. Menu text identifying the attachment provider. |

Source: https://developers.google.com/apps-script/manifest/calendar-addons
