# DirectionFinder

Allows for the retrieval of directions between locations.

Allows for the retrieval of directions between locations. The class enables users to specify origin, destination, and waypoints using addresses or coordinates, set travel modes and language preferences, and retrieve route details via the Google Directions API.

## Methods

### addWaypoint(latitude, longitude)

**Signature:** `addWaypoint(latitude: Number, longitude: Number): DirectionFinder`

**Description:** Adds a waypoint that the route must pass through, using a point (lat/lng). Returns the DirectionFinder object to facilitate method chaining.

### addWaypoint(address)

**Signature:** `addWaypoint(address: String): DirectionFinder`

**Description:** Adds a waypoint that the route must pass through, using an address. Returns the DirectionFinder object for chaining.

### clearWaypoints()

**Signature:** `clearWaypoints(): DirectionFinder`

**Description:** Clears the current set of waypoints. Removes all waypoints previously added with `addWaypoint()`. Returns the DirectionFinder object for chaining.

### getDirections()

**Signature:** `getDirections(): Object`

**Description:** Gets the directions using the origin, destination, and other options that were set. Returns a JSON object containing the set of routes, as described in the Google Directions API documentation.

### setAlternatives(useAlternatives)

**Signature:** `setAlternatives(useAlternatives: Boolean): DirectionFinder`

**Description:** Sets whether or not alternative routes should be returned, instead of just the highest ranked route (defaults to false). If true, the resulting object's routes array may contain multiple entries. Returns the DirectionFinder object for chaining.

### setArrive(time)

**Signature:** `setArrive(time: Date): DirectionFinder`

**Description:** Sets the desired time of arrival (when applicable). Returns the DirectionFinder object for chaining.

### setAvoid(avoid)

**Signature:** `setAvoid(avoid: String): DirectionFinder`

**Description:** Sets whether to avoid certain types of restrictions. Accepts a constant value from the Avoid enum. Returns the DirectionFinder object for chaining.

### setDepart(time)

**Signature:** `setDepart(time: Date): DirectionFinder`

**Description:** Sets the desired time of departure (when applicable). Returns the DirectionFinder object for chaining.

### setDestination(latitude, longitude)

**Signature:** `setDestination(latitude: Number, longitude: Number): DirectionFinder`

**Description:** Sets the ending location for which to calculate directions to, using a point (lat/lng). Returns the DirectionFinder object for chaining.

### setDestination(address)

**Signature:** `setDestination(address: String): DirectionFinder`

**Description:** Sets the ending location for which to calculate directions to, using an address. Returns the DirectionFinder object for chaining.

### setLanguage(language)

**Signature:** `setLanguage(language: String): DirectionFinder`

**Description:** Sets the language to be used for the directions. Accepts a BCP-47 language identifier. Returns the DirectionFinder object for chaining.

### setMode(mode)

**Signature:** `setMode(mode: String): DirectionFinder`

**Description:** Sets the mode of travel (defaults to driving). Accepts a constant value from the Mode enum. Returns the DirectionFinder object for chaining.

### setOptimizeWaypoints(optimizeOrder)

**Signature:** `setOptimizeWaypoints(optimizeOrder: Boolean): DirectionFinder`

**Description:** Sets whether or not to optimize the provided route by rearranging the waypoints in a more efficient order (defaults to false). Returns the DirectionFinder object for chaining.

### setOrigin(latitude, longitude)

**Signature:** `setOrigin(latitude: Number, longitude: Number): DirectionFinder`

**Description:** Sets the starting location from which to calculate directions, using a point (lat/lng). Returns the DirectionFinder object for chaining.

### setOrigin(address)

**Signature:** `setOrigin(address: String): DirectionFinder`

**Description:** Sets the starting location from which to calculate directions, using an address. Returns the DirectionFinder instance for chaining.

### setRegion(region)

**Signature:** `setRegion(region: String): DirectionFinder`

**Description:** Sets a region to use when interpreting location names. Region codes correspond to ccTLDs supported by Google Maps (e.g., "uk" for maps.google.co.uk). Returns the DirectionFinder object for chaining.
