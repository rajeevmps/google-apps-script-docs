# UserProperties

User Properties are key-value pairs unique to a user, scoped per user of the script.

User Properties are key-value pairs unique to a user. User Properties are scoped per user, meaning a script can only access properties for the user running the script.

**Deprecation note:** This class is deprecated and should not be used in new scripts. This is a legacy, standalone version of the properties API; new scripts should instead call `PropertiesService.getUserProperties()`, which returns a `Properties` object scoped to the current user (see `Properties.md` and `PropertiesService.md`). The methods and behavior documented below are for this legacy `UserProperties` class as returned/used directly (pre-`PropertiesService`), fetched verbatim from the current reference page at the URL below.

## Methods

### deleteAllProperties() → UserProperties

Deletes all properties.

See also: `deleteProperty(key)`

### deleteProperty(key: String) → UserProperties

Deletes the property with the given key.

See also: `deleteAllProperties()`

### getKeys() → String[]

Get all of the available keys.

### getProperties() → Object

Get all of the available properties at once. This gives a copy, not a live view, so changing the properties on the returned object won't update them in storage and vice versa.

### getProperty(key: String) → String|null

Returns the value associated with the provided key, or `null` if there is no such value.

### setProperties(properties: Object) → UserProperties

Bulk-sets all the properties drawn from the given object.

### setProperties(properties: Object, deleteAllOthers: Boolean) → UserProperties

Bulk-sets all the properties drawn from the given object.

### setProperty(key: String, value: String) → UserProperties

Persists the specified in value with the provided key. Any existing value associated with this key will be overwritten.

## Properties

(None)

## Code Sample

```javascript
UserProperties.setProperties({
  "cow"     : "moo",
  "sheep"   : "baa",
  "chicken" : "cluck"
});

Logger.log("A cow goes: %s", UserProperties.getProperty("cow"));

var animalSounds = UserProperties.getProperties();

for(var kind in animalSounds) {
  Logger.log("A %s goes %s!", kind, animalSounds[kind]);
}
```

Source: https://developers.google.com/apps-script/reference/properties/user-properties
