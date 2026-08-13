# PropertiesService

Allows scripts to store simple data in key-value pairs scoped to one script, one user of a script, or one document in which an add-on is used.

Allows scripts to store simple data in key-value pairs scoped to one script, one user of a script, or one document in which an add-on is used. Properties cannot be shared between scripts.

## Methods

### getDocumentProperties() → Properties

Gets a property store (for this script only) that all users can access within the open document, spreadsheet, or form. It is only available if the script is published and executing as an add-on or if it is bound to a Google file type. When document properties are not available this method returns `null`. Document properties created by a script are not accessible outside that script, even by other scripts accessing the same document.

### getScriptProperties() → Properties

Gets a property store that all users can access, but only within this script.

### getUserProperties() → Properties

Gets a property store that only the current or effective user can access, and only within this script.

## Properties

(None)

## Code Sample

```javascript
const documentProperties = PropertiesService.getDocumentProperties();
const scriptProperties = PropertiesService.getScriptProperties();
const userProperties = PropertiesService.getUserProperties();

documentProperties.setProperty('DAYS_TO_FETCH', '5');
scriptProperties.setProperty('SERVER_URL', 
    'http://www.example.com/MyWeatherService/');
userProperties.setProperty('DISPLAY_UNITS', 'metric');
```

Source: https://developers.google.com/apps-script/reference/properties/properties-service
