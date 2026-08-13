# Maps

Allows for direction finding, geocoding, elevation sampling and the creation of static map images.

Allows for direction finding, geocoding, elevation sampling and the creation of static map images.

## Properties

| Property | Type |
|----------|------|
| `DirectionFinder` | `DirectionFinderEnums` |
| `StaticMap` | `StaticMapEnums` |

## Methods

### decodePolyline(polyline)

**Signature:** `decodePolyline(polyline: String): Number[]`

**Description:** Decodes an encoded polyline string back into an array of points. Returns an array of latitude longitude pairs (lat0, long0, lat1, long1, ...).

**Code Sample:**
```javascript
const polyline = 'qvkpG`qhxPbgyI_zq_@';
const points = Maps.decodePolyline(polyline);
for (let i = 0; i < points.length; i += 2) {
  Logger.log('%s, %s', points[i], points[i + 1]);
}
```

### encodePolyline(points)

**Signature:** `encodePolyline(points: Number[]): String`

**Description:** Encodes an array of points into a string. Returns an encoded string representing those points.

**Code Sample:**
```javascript
const points = [40.77, -73.97, 42.34, -71.04];
const polyline = Maps.encodePolyline(points);
```

### newDirectionFinder()

**Signature:** `newDirectionFinder(): DirectionFinder`

**Description:** Creates a new DirectionFinder object.

### newElevationSampler()

**Signature:** `newElevationSampler(): ElevationSampler`

**Description:** Creates an ElevationSampler object.

### newGeocoder()

**Signature:** `newGeocoder(): Geocoder`

**Description:** Creates a new Geocoder object.

### newStaticMap()

**Signature:** `newStaticMap(): StaticMap`

**Description:** Creates a new StaticMap object.

### resetAuthenticationApiKey()

**Signature:** `resetAuthenticationApiKey(): void`

**Description:** Resets the authentication credentials to use the default quota allowances. This method works when you are using an API key to authenticate requests. Throws an error if `setAuthentication(clientId, signingKey)` is being used for authentication instead.

### setAuthenticationByApiKey(apiKey)

**Signature:** `setAuthenticationByApiKey(apiKey: String): void`

**Description:** Enables the use of an API key to authenticate requests to leverage additional quotas. Throws an error if apiKey is null, or if `setAuthentication()` is already in use.

**Code Sample:**
```javascript
Maps.setAuthenticationByApiKey('BBdgJpSbLtAtmkBFjgLt310qT6iekggfDdVqLC0');
```

### setAuthenticationByApiKey(apiKey, signingKey)

**Signature:** `setAuthenticationByApiKey(apiKey: String, signingKey: String): void`

**Description:** Enables the use of an API key and Signing Key to authenticate requests to leverage additional quotas in StaticMap. Throws an error if apiKey is null, or if `setAuthentication()` is already in use.

**Code Sample:**
```javascript
Maps.setAuthenticationByApiKey('BBdgJpSbLtAtmkBFjgLt310qT6iekggfDdVqLC0',
'7_pry-Skg0PKxds-7nvdl91mB5=');
```

### setAuthentication(clientId, signingKey) (Deprecated)

**Deprecated.** Use `setAuthenticationByApiKey(apiKey)` instead.

**Signature:** `setAuthentication(clientId: String, signingKey: String): void`

**Description:** Enables the use of an externally established Google Maps APIs Premium Plan account, to leverage additional quota allowances.

**Code Sample:**
```javascript
Maps.setAuthentication('gme-123456789', 'VhSEZvOXVSdnlxTnpJcUE');
```
