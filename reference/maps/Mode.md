# Mode

An enum representing the mode of travel to use when finding directions.

An enum representing the mode of travel to use when finding directions. Accessed via `Maps.Mode.[PROPERTY]`.

## Properties (Enum Values)

| Property | Description |
|----------|--------------|
| `DRIVING` | Driving directions via roads. |
| `WALKING` | Walking directions via pedestrian paths and sidewalks (where available). |
| `BICYCLING` | Bicycling directions via bicycle paths and preferred streets (where available). |
| `TRANSIT` | Transit directions via public transit routes (where available). This mode requires that you set either the departure or arrival time. |

## Code Sample

The documentation includes a code sample demonstrating transit directions from The Cloisters to JFK airport using `Maps.DirectionFinder.Mode.TRANSIT` with a departure time parameter.
