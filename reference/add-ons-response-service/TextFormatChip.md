# TextFormatChip

A clickable chip in the text format.

A clickable chip in the text format. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setLabel(label)

`setLabel(label: String): TextFormatChip`

Sets the text displayed in the chip.

**Parameters**
- `label` (String) — The text label of the chip.

**Returns**
- `TextFormatChip` — This chip object, for chaining.

### setTextFormatIcon(icon)

`setTextFormatIcon(icon: TextFormatIcon): TextFormatChip`

Sets the icon displayed in the chip.

**Parameters**
- `icon` (TextFormatIcon) — The `TextFormatIcon` to set in the chip.

**Returns**
- `TextFormatChip` — This chip object, for chaining.

### setUrl(url)

`setUrl(url: String): TextFormatChip`

Sets the URL to navigate to when the chip is clicked.

**Parameters**
- `url` (String) — The destination URL to the chip.

**Returns**
- `TextFormatChip` — This chip object, for chaining.

## Code Sample

```javascript
const chip = AddOnsResponseService.newChip()
    .setTextFormatIcon(AddOnsResponseService.newTextFormatIcon()
      .setIconUrl("https://www.google.com/icon.png"))
    .setLabel("test_label")
    .setUrl("https://www.google.com/chip.png");
```
