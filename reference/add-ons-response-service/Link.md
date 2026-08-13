# Link

The link object from a third-party resource which gets converted to a smart chip.

The link object from a third-party resource which gets converted it to a smart chip in the host application. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setTitle(title)

`setTitle(title: String): Link`

Sets the title of the link.

**Parameters**
- `title` (String) — The displayed title of this link object.

**Returns**
- `Link` — This link object, for chaining.

### setUrl(url)

`setUrl(url: String): Link`

Sets the URL of the link.

**Parameters**
- `url` (String) — The destination URL of the link object.

**Returns**
- `Link` — This link object, for chaining.

## Code Sample

```javascript
const link = AddOnsResponseService.newLink()
    .setUrl("www.clickme.com");
```
