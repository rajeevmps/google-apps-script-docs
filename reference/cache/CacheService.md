# CacheService

Allows you to access a cache for short term storage of data.

CacheService allows you to access a cache for short term storage of data. This class lets you get a specific cache instance. Public caches are for things that are not dependent on which user is accessing your script. Private caches are for things which are user-specific, like settings or recent activity. The data you write to the cache is not guaranteed to persist until its expiration time. You must be prepared to get back `null` from all reads.

## Methods

| Method | Return Type | Brief Description |
|--------|-------------|-------------------|
| `getDocumentCache()` | `Cache` | Gets the cache instance scoped to the current document and script. |
| `getScriptCache()` | `Cache` | Gets the cache instance scoped to the script. |
| `getUserCache()` | `Cache` | Gets the cache instance scoped to the current user and script. |

### getDocumentCache() → Cache

Gets the cache instance scoped to the current document and script. Document caches are specific to the current document which contains the script. Use these to store script information that is specific to the current document. If this method is called outside of the context of a containing document (such as from a standalone script or web app), this method returns `null`.

**Return**

`Cache` — A document cache instance, or `null` if there is no containing document.

```javascript
// Gets a cache that is specific to the current document containing the script
const cache = CacheService.getDocumentCache();
```

### getScriptCache() → Cache

Gets the cache instance scoped to the script. Script caches are common to all users of the script. Use these to store information that is not specific to the current user.

**Return**

`Cache` — A script cache instance.

```javascript
// Gets a cache that is common to all users of the script
const cache = CacheService.getScriptCache();
```

### getUserCache() → Cache

Gets the cache instance scoped to the current user and script. User caches are specific to the current user of the script. Use these to store script information that is specific to the current user.

**Return**

`Cache` — A user cache instance.

```javascript
// Gets a cache that is specific to the current user of the script
const cache = CacheService.getUserCache();
```

## Properties

None.

---

Source: https://developers.google.com/apps-script/reference/cache/cache-service
