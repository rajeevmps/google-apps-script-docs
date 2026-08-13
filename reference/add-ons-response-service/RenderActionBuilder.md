# RenderActionBuilder

A builder for `RenderAction` objects.

A builder for `RenderAction` objects. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### build()

`build(): RenderAction`

Builds the current render action and validates it.

**Returns**
- `RenderAction` — A validated `RenderAction` object.

### setAction(action)

`setAction(action: Action): RenderActionBuilder`

Sets the action that add-ons can use to update the UI to the render action.

**Parameters**
- `action` (Action) — The action to use.

**Returns**
- `RenderActionBuilder` — This render action builder, for chaining.

### setHostAppAction(hostAppAction)

`setHostAppAction(hostAppAction: HostAppAction): RenderActionBuilder`

Sets the `HostAppAction` handled by individual host apps to the render action.

**Parameters**
- `hostAppAction` (HostAppAction) — The `HostAppAction` to send to the host app.

**Returns**
- `RenderActionBuilder` — This render action builder, for chaining.
