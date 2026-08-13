# ElevationSampler

Allows for the sampling of elevations at particular locations.

Allows for the sampling of elevations at particular locations. The class enables developers to query elevation data from the Google Elevation API through Apps Script's Maps service.

## Methods

### sampleLocation(latitude, longitude)

**Signature:** `sampleLocation(latitude: Number, longitude: Number): Object`

**Description:** Returns elevation information for a single geographic point specified by latitude and longitude coordinates. Returns a JSON object containing elevation data as documented in the Google Elevation API response format.

### sampleLocations(points)

**Signature:** `sampleLocations(points: Number[]): Object`

**Description:** Returns elevation information for multiple points provided as an array of latitude/longitude pairs. Returns a JSON object containing elevation data for each sampled location.

### sampleLocations(encodedPolyline)

**Signature:** `sampleLocations(encodedPolyline: String): Object`

**Description:** Returns elevation information for points encoded within a polyline string format. Returns a JSON object containing elevation data for each point in the polyline.

### samplePath(points, numSamples)

**Signature:** `samplePath(points: Number[], numSamples: Integer): Object`

**Description:** Returns elevation data sampled at regular intervals along a path defined by multiple coordinate points. Returns a JSON object containing elevation information distributed across the specified path.

### samplePath(encodedPolyline, numSamples)

**Signature:** `samplePath(encodedPolyline: String, numSamples: Integer): Object`

**Description:** Returns elevation data sampled at regular intervals along a path encoded as a polyline. Returns a JSON object containing elevation data distributed across the encoded path.
