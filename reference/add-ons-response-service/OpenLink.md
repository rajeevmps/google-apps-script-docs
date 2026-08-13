# OpenLink

Represents an action to open a link with some options.

Represents an action to open a link with some options. Available for Google Workspace add-ons and Google Chat apps.

## Methods

### setOnClose(onClose)

`setOnClose(onClose: OnClose): OpenLink`

Sets the behavior of the URL action when the URL window or tab is closed.

**Parameters**
- `onClose` (OnClose) — The closing setting.

**Returns**
- `OpenLink` — This object, for chaining.

### setOpenAs(openAs)

`setOpenAs(openAs: OpenAs): OpenLink`

Sets the behavior of URL when it is opened.

**Parameters**
- `openAs` (OpenAs) — The opening setting.

**Returns**
- `OpenLink` — This object, for chaining.

### setUrl(url)

`setUrl(url: String): OpenLink`

Sets the URL to be opened. The URL must match a prefix whitelisted in the manifest.

**Parameters**
- `url` (String) — The destination URL to open.

**Returns**
- `OpenLink` — This object, for chaining.

## Code Samples

Two examples are shown on the reference page: button creation with OpenLink (overlay mode with reload) and ActionResponse creation (full screen mode with no close action).

Note: To reload add-ons after closing a link, don't use a link with Cross-Origin-Opener-Policy header enabled.
