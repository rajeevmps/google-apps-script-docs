# Cache

A reference to a particular cache.

A reference to a particular cache. This class allows you to insert, retrieve, and remove items from a cache. Caches are common to the script, and are frequently used to store the results of expensive calls or fetches for reuse.

## Methods

| Method | Return Type | Brief Description |
|--------|-------------|-------------------|
| `get(key)` | `String\|null` | Gets the cached value for the given key, or `null` if none is found. |
| `getAll(keys)` | `Object` | Returns a JavaScript Object containing all key/value pairs found in the cache for an array of keys. |
| `put(key, value)` | `void` | Adds a key/value pair to the cache. |
| `put(key, value, expirationInSeconds)` | `void` | Adds a key/value pair to the cache, with an expiration time (in seconds). |
| `putAll(values)` | `void` | Adds a set of key/value pairs to the cache. |
| `putAll(values, expirationInSeconds)` | `void` | Adds a set of key/value pairs to the cache, with an expiration time (in seconds). |
| `remove(key)` | `void` | Removes an entry from the cache using the given key. |
| `removeAll(keys)` | `void` | Removes a set of entries from the cache. |

### get(key: String) → String|null

Gets the cached value for the given key, or `null` if none is found.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| `key` | `String` | The key to look up in the cache. |

**Return**

`String|null` — The cached value, or `null` if none was found.

```javascript
const value = CacheService.getScriptCache().get('foo');
```

### getAll(keys: String[]) → Object

Returns a JavaScript Object containing all key/value pairs found in the cache for an array of keys.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| `keys` | `String[]` | The keys to lookup. |

**Return**

`Object` — A JavaScript Object containing the key/value pairs for all keys found in the cache.

```javascript
const values = CacheService.getDocumentCache().getAll(['foo', 'x', 'missing']);
```

### put(key: String, value: String) → void

Adds a key/value pair to the cache. The maximum length of a key is 250 characters. The maximum amount of data that can be stored per key is 100KB. The value expires from the cache after 600 seconds (10 minutes). The cap for cached items is 1,000.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| `key` | `String` | The key to store the value under. |
| `value` | `String` | The value to be cached. |

**Return**

`void`

```javascript
const cache = CacheService.getScriptCache();
cache.put('foo', 'bar');
```

### put(key: String, value: String, expirationInSeconds: Integer) → void

Adds a key/value pair to the cache, with an expiration time (in seconds). The maximum length of a key is 250 characters. The maximum amount of data that can be stored per key is 100KB. The specified expiration time is only a suggestion; cached data may be removed before this time if a lot of data is cached.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| `key` | `String` | The key to store the value under. |
| `value` | `String` | The value to be cached. |
| `expirationInSeconds` | `Integer` | The maximum time the value remains in the cache, in seconds. The minimum is 1 second and the maximum is 21600 seconds (6 hours). |

**Return**

`void`

```javascript
CacheService.getScriptCache().put('foo', 'bar', 20);
```

### putAll(values: Object) → void

Adds a set of key/value pairs to the cache. Similar to repeated calls to 'put', but more efficient as it only makes one call to the memcache server to set all values. The maximum length of a key is 250 characters. The maximum amount of data that can be stored per key is 100KB. The values expire from the cache after 600 seconds (10 minutes). The cap for cached items is 1,000.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| `values` | `Object` | A JavaScript Object containing string keys and values. |

**Return**

`void`

```javascript
const values = {
  foo: 'bar',
  x: 'y',
  key: 'value',
};
CacheService.getUserCache().putAll(values);
```

### putAll(values: Object, expirationInSeconds: Integer) → void

Adds a set of key/value pairs to the cache, with an expiration time (in seconds). Similar to repeated calls to 'put', but more efficient as it only makes one call to the memcache server to set all values. The maximum length of a key is 250 characters. The maximum amount of data that can be stored per key is 100KB.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| `values` | `Object` | A JavaScript Object containing string keys and values. |
| `expirationInSeconds` | `Integer` | The maximum time the value remains in the cache, in seconds. The minimum allowed expiration is 1 second, and the maximum allowed expiration is 21600 seconds (6 hours). The default expiration is 600 seconds (10 minutes). |

**Return**

`void`

```javascript
const values = {
  foo: 'bar',
  x: 'y',
  key: 'value',
};
CacheService.getUserCache().putAll(values, 20);
```

### remove(key: String) → void

Removes an entry from the cache using the given key.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| `key` | `String` | The key to remove from the cache. |

**Return**

`void`

```javascript
CacheService.getUserCache().remove('foo');
```

### removeAll(keys: String[]) → void

Removes a set of entries from the cache.

**Parameters**

| Name | Type | Description |
|------|------|-------------|
| `keys` | `String[]` | The array of keys to remove. |

**Return**

`void`

```javascript
CacheService.getDocumentCache().removeAll(['foo', 'x']);
```

## Properties

None.

---

Source: https://developers.google.com/apps-script/reference/cache/cache
