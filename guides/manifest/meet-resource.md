# Meet Manifest Resource Documentation

## Meet

The Google Workspace add-on manifest configuration for Google Meet extensions. See [Extending Meet with Google Workspace add-ons](https://developers.google.com/workspace/meet/add-ons/guides/overview) for details.

**JSON representation**

```json
{
  "web": {
    object (Web)
  },
  "homepageTrigger": {
    object (HomepageTrigger)
  }
}
```

**Fields**

| Field | Type | Description |
|-------|------|-------------|
| `web` | object (Web) | **Required.** Web configuration for the Meet Google Workspace add-on. |
| `homepageTrigger` | object (HomepageTrigger) | The trigger function for the add-on [homepage](https://developers.google.com/workspace/add-ons/concepts/homepages) in the Meet host. This overrides `addOns.common.homepageTrigger`. |

---

## Web

Web execution properties.

**JSON representation**

```json
{
  "sidePanelUrl": string,
  "supportsScreenSharing": boolean,
  "addOnOrigins": [
    {
      string: string,
      ...
    }
  ],
  "logoUrl": string,
  "darkModeLogoUrl": string
}
```

**Fields**

| Field | Type | Description |
|-------|------|-------------|
| `sidePanelUrl` | string | **Required.** The URL for the side panel iframe. This is the entry point for your add-on app. |
| `supportsScreenSharing` | boolean | **Required.** Whether the add-on supports screen sharing. If `false`, users must use the add-on to see activity in a collaborative session. If `true`, the initiator can screen share their view of the add-on. |
| `addOnOrigins` | string | **Required.** An array of origins where your add-on is hosted. Sub-origins and wildcard subdomains are permitted. See [Add-on security](https://developers.google.com/workspace/meet/add-ons/guides/add-on-security) for details. |
| `logoUrl` | string | **Required.** A Meet-specific URL of the logo. This logo is used throughout Meet. If omitted, the logo defaults to the common section logo. |
| `darkModeLogoUrl` | string | Optional. A dark mode specific URL of the logo. |

Source: https://developers.google.com/apps-script/manifest/meet-addons
