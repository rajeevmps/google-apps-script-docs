# Geocoder

Allows for the conversion between an address and geographical coordinates.

Allows for the conversion between an address and geographical coordinates. The Geocoder class enables developers to convert addresses to geographic coordinates and vice versa.

## Methods

### geocode(address)

**Signature:** `geocode(address: String): Object`

**Description:** Gets the approximate geographic points for a given address. Returns a JSON object containing geocoding data matching the address parameter provided.

**Code Sample:**
```javascript
const response = Maps.newGeocoder().geocode('Times Square, New York, NY');
for (let i = 0; i < response.results.length; i++) {
  const result = response.results[i];
  Logger.log(
      '%s: %s, %s',
      result.formatted_address,
      result.geometry.location.lat,
      result.geometry.location.lng,
  );
}
```

### reverseGeocode(latitude, longitude)

**Signature:** `reverseGeocode(latitude: Number, longitude: Number): Object`

**Description:** Gets the approximate addresses for a given geographic point. Returns reverse geocoding data for the specified coordinates.

**Code Sample:**
```javascript
const response = Maps.newGeocoder().reverseGeocode(40.758577, -73.984464);
for (let i = 0; i < response.results.length; i++) {
  const result = response.results[i];
  Logger.log(
      '%s: %s, %s',
      result.formatted_address,
      result.geometry.location.lat,
      result.geometry.location.lng,
  );
}
```

### setBounds(swLatitude, swLongitude, neLatitude, neLongitude)

**Signature:** `setBounds(swLatitude: Number, swLongitude: Number, neLatitude: Number, neLongitude: Number): Geocoder`

**Description:** Sets the bounds of an area that should be given extra preference in the results. Enables method chaining.

### setLanguage(language)

**Signature:** `setLanguage(language: String): Geocoder`

**Description:** Sets the language to be used in the results. Accepts BCP-47 language identifiers. Enables method chaining.

### setRegion(region)

**Signature:** `setRegion(region: String): Geocoder`

**Description:** Sets a region to use when interpreting location names. Region codes correspond to ccTLDs supported by Google Maps. Enables method chaining.
