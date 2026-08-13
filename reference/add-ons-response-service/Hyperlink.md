# Hyperlink

A Hyperlink element used in `TextFormatElement`.

A Hyperlink element used in `TextFormatElement`. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setLink(link)

`setLink(link: String): Hyperlink`

Sets the destination URL of the hyperlink.

**Parameters**
- `link` (String) — The destination URL of the hyperlink.

**Returns**
- `Hyperlink` — This hyperlink object, for chaining.

### setText(text)

`setText(text: String): Hyperlink`

Sets the text of the hyperlink.

**Parameters**
- `text` (String) — The text of the hyperlink.

**Returns**
- `Hyperlink` — This hyperlink object, for chaining.

## Code Sample

```javascript
const hyperLink = AddOnsResponseService.newHyperlink()
      .setText("Hyperlink_text")
      .setLink("https://www.google.com");
```
