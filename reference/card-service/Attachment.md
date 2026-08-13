# Attachment

Represents an attachment created by an add-on.

Represents an attachment created by an add-on. This can be used within the context of different Google extensibility products to generate new attachments, such as for Calendar events.

```javascript
const attachment = CardService.newAttachment()
                       .setResourceUrl('https://fakeresourceurl.com')
                       .setTitle('Attachment title')
                       .setMimeType('text/html')
                       .setIconUrl('https://fakeresourceurl.com/iconurl.png');
```

## Methods

### setIconUrl(iconUrl: String): Attachment

Sets the icon URL for the attachment.

Parameters:
- `iconUrl` (String): The URL address of the attachment icon.

Returns: This object, for chaining.

### setMimeType(mimeType: String): Attachment

Sets the MIME type for the attachment.

Parameters:
- `mimeType` (String): The MIME type of the content in the attachment resource.

Returns: This object, for chaining.

### setResourceUrl(resourceUrl: String): Attachment

Sets the resource URL for the attachment.

Parameters:
- `resourceUrl` (String): The URL address of a resource.

Returns: This object, for chaining.

### setTitle(title: String): Attachment

Sets the title for the attachment.

Parameters:
- `title` (String): The title of the attachment.

Returns: This object, for chaining.
