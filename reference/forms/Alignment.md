# Alignment

An enum representing the supported types of image alignment.

An enum representing the supported types of image alignment. Alignment types can be accessed from `FormApp.Alignment`.

To invoke an enum value, use the pattern: `FormApp.Alignment.PROPERTY_NAME`

## Code Sample

```javascript
// Open a form by ID and add a new image item with alignment
const form = FormApp.openById('1234567890abcdefghijklmnopqrstuvwxyz');
const img = UrlFetchApp.fetch('https://www.google.com/images/srpr/logo4w.png');
form.addImageItem().setImage(img).setAlignment(FormApp.Alignment.CENTER);
```

## Properties

| Property | Description |
| --- | --- |
| `LEFT` | Align the image to the left side of the form. |
| `CENTER` | Align the image to the center of the form. |
| `RIGHT` | Align the image to the right side of the form. |
