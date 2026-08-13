# TextFormatIcon

An icon that is displayed in a `TextFormatChip`.

An icon that is displayed in a `TextFormatChip`. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setIconUrl(iconUrl)

`setIconUrl(iconUrl: String): TextFormatIcon`

Sets the icon URL.

**Parameters**
- `iconUrl` (String) — The destination URL of the icon.

**Returns**
- `TextFormatIcon` — This text format icon object.

### setMaterialIconName(materialIconName)

`setMaterialIconName(materialIconName: String): TextFormatIcon`

Sets the material icon name defined in Google Material Icons.

**Parameters**
- `materialIconName` (String) — The material icon name to set.

**Returns**
- `TextFormatIcon` — This text format icon object.

## Code Sample

```javascript
const icon = AddOnsResponseService.newTextFormatIcon()
      .setMaterialIconName("check_box");
```
