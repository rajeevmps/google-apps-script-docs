# StaticMap

Allows for the creation and decoration of static map images.

Allows for the creation and decoration of static map images. You can configure size, center point, markers, and paths. Markers and visible locations support both latitude/longitude coordinates and addresses. Paths can use addresses, points, or encoded polylines. The `getMapUrl()` method retrieves the generated map URL but requires an API key.

## Methods

### addAddress(address)

**Signature:** `addAddress(address: String): StaticMap`

**Description:** Adds a new address to the current path definition. Used within a `beginPath()`/`endPath()` block to define path vertices.

### addMarker(latitude, longitude)

**Signature:** `addMarker(latitude: Number, longitude: Number): StaticMap`

**Description:** Adds a marker to the map using a point (lat/lng).

### addMarker(address)

**Signature:** `addMarker(address: String): StaticMap`

**Description:** Adds a marker to the map using an address.

### addPath(points)

**Signature:** `addPath(points: Number[]): StaticMap`

**Description:** Adds a path to the map using an array of points.

### addPath(polyline)

**Signature:** `addPath(polyline: String): StaticMap`

**Description:** Adds a path to the map using an encoded polyline.

### addPoint(latitude, longitude)

**Signature:** `addPoint(latitude: Number, longitude: Number): StaticMap`

**Description:** Adds a new point (lat/lng) to the current path definition.

### addVisible(latitude, longitude)

**Signature:** `addVisible(latitude: Number, longitude: Number): StaticMap`

**Description:** Adds a point (lat/lng) location that must be visible in the map.

### addVisible(address)

**Signature:** `addVisible(address: String): StaticMap`

**Description:** Adds an address location that must be visible in the map.

### beginPath()

**Signature:** `beginPath(): StaticMap`

**Description:** Starts a new path definition. Calls to `addAddress()` and `addPoint()` define each new vertex in the path. The path is completed when `endPath()` is called.

### clearMarkers()

**Signature:** `clearMarkers(): StaticMap`

**Description:** Clears the current set of markers.

### clearPaths()

**Signature:** `clearPaths(): StaticMap`

**Description:** Clear the current set of paths.

### clearVisibles()

**Signature:** `clearVisibles(): StaticMap`

**Description:** Clears the current set of visible locations.

### endPath()

**Signature:** `endPath(): StaticMap`

**Description:** Completes a path definition started with `beginPath()`.

### getAs(contentType)

**Signature:** `getAs(contentType: String): Blob`

**Description:** Return the data inside this object as a blob converted to the specified content type. This method adds the appropriate extension to the filename.

### getBlob()

**Signature:** `getBlob(): Blob`

**Description:** Gets the image data as a `Blob`.

### getMapImage()

**Signature:** `getMapImage(): Byte[]`

**Description:** Gets the raw image data as a byte array. In general, prefer using `getBlob()` which allows for simpler interactions with other services.

### getMapUrl()

**Signature:** `getMapUrl(): String`

**Description:** Gets the URL of the map image.

### setCenter(latitude, longitude)

**Signature:** `setCenter(latitude: Number, longitude: Number): StaticMap`

**Description:** Sets the center of the map using a point (lat/lng).

### setCenter(address)

**Signature:** `setCenter(address: String): StaticMap`

**Description:** Sets the center of the map using an address.

### setCustomMarkerStyle(imageUrl, useShadow)

**Signature:** `setCustomMarkerStyle(imageUrl: String, useShadow: Boolean): StaticMap`

**Description:** Sets the custom marker image to use when creating new markers. Markers that have already been added are not affected.

### setFormat(format)

**Signature:** `setFormat(format: String): StaticMap`

**Description:** Sets the format of the map image.

### setLanguage(language)

**Signature:** `setLanguage(language: String): StaticMap`

**Description:** Sets the language to be used for text on the map (where available).

### setMapType(mapType)

**Signature:** `setMapType(mapType: String): StaticMap`

**Description:** Sets the type of map to be shown.

### setMarkerStyle(size, color, label)

**Signature:** `setMarkerStyle(size: String, color: String, label: String): StaticMap`

**Description:** Sets the marker style to use when creating new markers. Markers that have already been added are not affected.

### setMobile(useMobileTiles)

**Signature:** `setMobile(useMobileTiles: Boolean): StaticMap`

**Description:** Sets whether or not to use specialized tile sets for mobile devices.

### setPathStyle(weight, color, fillColor)

**Signature:** `setPathStyle(weight: Integer, color: String, fillColor: String): StaticMap`

**Description:** Sets the path style to use when creating new paths. Paths that have already been added are not affected.

### setSize(width, height)

**Signature:** `setSize(width: Integer, height: Integer): StaticMap`

**Description:** Sets the width and height of the map image in pixels.

### setZoom(zoom)

**Signature:** `setZoom(zoom: Integer): StaticMap`

**Description:** Sets the zoom factor, or magnification level, used for the map.
