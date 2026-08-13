# Properties

The properties object allows access to user, document, or script properties through methods of the PropertiesService.

The properties object allows access to user, document, or script properties through methods of the `PropertiesService`. Properties cannot be shared between different scripts. The `Properties` object includes methods for deleting properties, retrieving keys or all properties, and setting individual or multiple properties.

The properties object serves as the interface to access user, document, or script properties. The specific property type depends on which of the three methods of `PropertiesService` the script called: `getDocumentProperties()`, `getUserProperties()`, or `getScriptProperties()`. Properties cannot be shared between scripts.

## Methods

### deleteAllProperties() → Properties

Deletes all properties in the current `Properties` store.

Returns: this `Properties` store, for chaining

```javascript
const userProperties = PropertiesService.getUserProperties();
userProperties.deleteAllProperties();
```

### deleteProperty(key: String) → Properties

Deletes the property with the given key in the current `Properties` store.

Parameters:
- `key` (String) — the key for the property to delete

Returns: this `Properties` store, for chaining

```javascript
const userProperties = PropertiesService.getUserProperties();
userProperties.deleteProperty('nickname');
```

### getKeys() → String[]

Gets all keys in the current `Properties` store.

Returns: an array of all keys in the current `Properties` store

```javascript
const scriptProperties = PropertiesService.getScriptProperties();
scriptProperties.setProperties({
  cow: 'moo',
  sheep: 'baa',
  chicken: 'cluck',
});
const keys = scriptProperties.getKeys();
Logger.log('Animals known:');
for (let i = 0; i < keys.length; i++) {
  Logger.log(keys[i]);
}
```

### getProperties() → Object

Gets a copy of all key-value pairs in the current `Properties` store. Note that the returned object is not a live view of the store. Consequently, changing the properties on the returned object will not automatically update them in storage, or vice versa.

Returns: a copy of all key-value pairs in the current `Properties` store

```javascript
const scriptProperties = PropertiesService.getScriptProperties();
scriptProperties.setProperties({
  cow: 'moo',
  sheep: 'baa',
  chicken: 'cluck',
});

const animalSounds = scriptProperties.getProperties();

for (const kind in animalSounds) {
  Logger.log('A %s goes %s!', kind, animalSounds[kind]);
}
```

### getProperty(key: String) → String

Gets the value associated with the given key in the current `Properties` store, or `null` if no such key exists.

Parameters:
- `key` (String) — the key for the property value to retrieve

Returns: the value associated with the given key in the current `Properties` store

```javascript
const userProperties = PropertiesService.getUserProperties();
const nickname = userProperties.getProperty('nickname');
Logger.log(nickname);
```

### setProperties(properties: Object) → Properties

Sets all key-value pairs from the given object in the current `Properties` store.

Parameters:
- `properties` (Object) — an object containing key-values pairs to set

Returns: this `Properties` store, for chaining

```javascript
const userProperties = PropertiesService.getUserProperties();
const newProperties = {
  nickname: 'Bob',
  region: 'US',
  language: 'EN'
};
userProperties.setProperties(newProperties);
```

### setProperties(properties: Object, deleteAllOthers: Boolean) → Properties

Sets all key-value pairs from the given object in the current `Properties` store, optionally deleting all other properties in the store.

Parameters:
- `properties` (Object) — an object containing key-values pairs to set
- `deleteAllOthers` (Boolean) — `true` to delete all other key-value pairs in the properties object; `false` to not

Returns: this `Properties` store, for chaining

```javascript
const userProperties = PropertiesService.getUserProperties();
const newProperties = {
  nickname: 'Bob',
  region: 'US',
  language: 'EN'
};
userProperties.setProperties(newProperties, true);
```

### setProperty(key: String, value: String) → Properties

Sets the given key-value pair in the current `Properties` store.

Parameters:
- `key` (String) — the key for the property
- `value` (String) — the value to associate with the key

Returns: this `Properties` store, for chaining

```javascript
const userProperties = PropertiesService.getUserProperties();
userProperties.setProperty('nickname', 'Bobby');
```

## Properties

(None)

Source: https://developers.google.com/apps-script/reference/properties/properties
