# ScriptProperties

Script Properties are key-value pairs stored by a script in a persistent store, scoped per script.

Script Properties are key-value pairs stored by a script in a persistent store. Script Properties are scoped per script, regardless of which user runs the script.

**Deprecation note:** The ScriptProperties class is deprecated and should not be used in new scripts. This is a legacy, standalone version of the properties API; new scripts should instead call `PropertiesService.getScriptProperties()`, which returns a `Properties` object scoped to the script (see `Properties.md` and `PropertiesService.md`). The methods and behavior documented below are for this legacy `ScriptProperties` class as returned/used directly (pre-`PropertiesService`), fetched verbatim from the current reference page at the URL below.

## Methods

### deleteAllProperties() → ScriptProperties

Deletes all properties.

### deleteProperty(key: String) → ScriptProperties

Deletes the property with the given key.

### getKeys() → String[]

Get all of the available keys.

### getProperties() → Object

Get all of the available properties at once. This gives a copy, not a live view, so changing the properties on the returned object won't update them in storage and vice versa.

### getProperty(key: String) → String|null

Returns the value associated with the provided key, or `null` if there is no such value.

### setProperties(properties: Object) → ScriptProperties

Bulk-sets all the properties drawn from the given object.

### setProperties(properties: Object, deleteAllOthers: Boolean) → ScriptProperties

Bulk-sets all the properties drawn from the given object.

### setProperty(key: String, value: String) → ScriptProperties

Persists the specified in value with the provided key. Any existing value associated with this key will be overwritten.

## Properties

(None)

## Code Samples

```javascript
ScriptProperties.setProperties({
  "cow"     : "moo",
  "sheep"   : "baa",
  "chicken" : "cluck"
});

Logger.log("A cow goes: %s", ScriptProperties.getProperty("cow"));

var animalSounds = ScriptProperties.getProperties();

for(var kind in animalSounds) {
  Logger.log("A %s goes %s!", kind, animalSounds[kind]);
}
```

```javascript
const specialValue = ScriptProperties.getProperty('special');
```

```javascript
ScriptProperties.setProperty('special', 'sauce');
```

```javascript
ScriptProperties.setProperties({special: 'sauce', 'meaning': 42});
```

```javascript
ScriptProperties.setProperties({special: 'sauce', 'meaning': 42}, true);
```

```javascript
ScriptProperties.deleteProperty('special');
```

Source: https://developers.google.com/apps-script/reference/properties/script-properties
