# CardHeader

The header of a `Card`.

The header of a `Card`. Available for Google Workspace add-ons and Google Chat apps.

```javascript
const cardHeader = CardService.newCardHeader()
                       .setTitle('Card header title')
                       .setSubtitle('Card header subtitle')
                       .setImageStyle(CardService.ImageStyle.CIRCLE)
                       .setImageUrl('https://image.png');
```

## Methods

### setImageAltText(imageAltText: String): CardHeader

Sets the alternative text for the header image.

### setImageStyle(imageStyle: ImageStyle): CardHeader

Sets the cropping of the icon in the card header. Defaults to no crop. Optional.

### setImageUrl(imageUrl: String): CardHeader

Sets the image to use in the header by providing its URL or data string. The provided URL can either be a publicly accessible URL or a base64 encoded image string.

### setSubtitle(subtitle: String): CardHeader

Sets the subtitle of the card header. Optional.

### setTitle(title: String): CardHeader

Sets the title of the card header. Required.
