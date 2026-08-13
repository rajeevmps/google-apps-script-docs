# RenderAction

Renders or updates a card by performing an `Action` in response to a user interaction.

Renders or updates a card by performing an `Action` in response to a user interaction. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### printJson()

`printJson(): String`

Prints the JSON representation of this object. This is for debugging only.

## Code Sample

```javascript
const renderAction = AddOnsResponseService.newRenderActionBuilder()
.setAction(AddOnsResponseService.newAction().setLink(AddOnsResponseService.newLink().setUrl('https://www.google.com')))
.build();
```
