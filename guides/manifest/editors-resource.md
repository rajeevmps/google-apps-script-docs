# Editor Manifest Resource Documentation

## Editors

**Description:** The Google Workspace add-on manifest configuration for Editor extensions. See [Extending Editors with Google Workspace add-ons](https://developers.google.com/workspace/add-ons/editors/gsao) for details.

**JSON Representation:**
```json
{
  "homepageTrigger": {
    object (HomepageTrigger)
  },
  "onFileScopeGrantedTrigger": {
    object (OnFileScopeGrantedTrigger)
  },
  "linkPreviewTriggers": [
    {
      object (LinkPreviewTriggers)
    }
  ],
  "createActionTriggers": [
    {
      object (CreateActionTriggers)
    }
  ]
}
```

**Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `homepageTrigger` | object (HomepageTrigger) | This trigger function creates the add-on homepage in the host app. This overrides `addOns.common.homepageTrigger`. |
| `onFileScopeGrantedTrigger` | object (OnFileScopeGrantedTrigger) | Required if the add-on includes behavior specific to the current document, triggered when the user authorizes the `drive.file` scope. |
| `linkPreviewTriggers[]` | object (LinkPreviewTriggers) | Required for link previews. A list of triggers for previewing links in a Google Docs, Sheets, or Slides file. |
| `createActionTriggers[]` | object (CreateActionTriggers) | Required for third-party resource creation. A list of triggers for creating resources in a third-party service from the @ menu. |

---

## OnFileScopeGrantedTrigger

**Description:** A configuration for a contextual trigger that fires when the request file scope dialog uses `CardService.newEditorFileScopeActionResponseBuilder().requestFileScopeForActiveDocument().build();` and the user grants `drive.file` scope authorization.

**JSON Representation:**
```json
{
  "runFunction": string
}
```

**Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `runFunction` | string | The name of the function to run if `drive.file` scope is granted. The function must return an array of Card objects for the UI. |

---

## LinkPreviewTriggers

**Description:** The configuration for a trigger that fires when a user types or pastes a link from a third-party service into a Docs, Sheets, or Slides file.

**JSON Representation:**
```json
{
  "labelText": string,
  "localizedLabelText": {
    string: string,
    ...
  },
  "runFunction": string,
  "logoUrl": string,
  "patterns": [
    {
      object(UriPattern)
    }
  ]
}
```

**Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `labelText` | string | Required. The text for an example smart chip prompting users to preview the link, such as `Example: Support case`. This text is static. |
| `localizedLabelText` | map (key: string, value: string) | Optional. A map of `labelText` to localize into other languages. Format the language in ISO 639 and country/region in ISO 3166, separated by a hyphen `-`. |
| `patterns[]` | object (UriPattern) | Required. An array of URL patterns that trigger the add-on to preview links. |
| `runFunction` | string | Required. The name of the function to run when the user authorizes the `https://www.googleapis.com/auth/workspace.linkpreview` scope. The function must accept an event object, which includes a `matchedUrl.url` property containing the URL to preview, and return a Card object. |
| `logoUrl` | string | Optional. The icon displaying in the smart chip and preview card. If omitted, the add-on uses its toolbar icon, `logoUrl`. |

---

## UriPattern

**Description:** The configuration for each URL pattern that triggers a link preview.

**JSON Representation:**
```json
{
  "hostPattern": string,
  "pathPrefix" : string
}
```

**Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `hostPattern` | string | Required for each URL pattern. The URL pattern domain. The add-on previews links containing this domain. To match all subdomains, use a wildcard asterisk (`*`). |
| `pathPrefix` | string | Optional. The path appending the domain. To match all URLs in the domain, leave `pathPrefix` empty. |

---

## CreateActionTriggers

**Description:** The configuration for a trigger that fires when a user selects a third-party integration menu item from the Google Docs @ menu.

**JSON Representation:**
```json
{
  "id": string,
  "labelText": string,
  "localizedLabelText": {
    string: string,
    ...
  },
  "runFunction": string,
  "logoUrl": string,
}
```

**Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Required. The unique ID for this extension point. Use up to 64 characters in `[a-zA-Z0-9-]+.` format. |
| `labelText` | string | Required. The text appearing in the @ menu, such as `Create support case`. |
| `localizedLabelText` | map (key: string, value: string) | Optional. A map of `labelText` to localize. Format the language in ISO 639 and country/region in ISO 3166, separated by a hyphen `-`. |
| `runFunction` | string | Required. The name of the function to run when a user selects an extension point. The function must return a form card. |
| `logoUrl` | string | Optional. The icon that displays in the @ menu. If omitted, the add-on uses its toolbar icon, `logoUrl`. |

Source: https://developers.google.com/apps-script/manifest/editor-addons
