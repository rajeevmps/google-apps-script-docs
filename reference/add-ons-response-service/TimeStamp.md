# TimeStamp

Represents a timestamp object which can be added to a `VariableData`.

Represents a timestamp object which is can be added to a `VariableData`. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setNanos(nanos)

`setNanos(nanos: Integer): TimeStamp`

Sets the nanos of the timestamp, it represents the number of nanoseconds within the current second.

**Parameters**
- `nanos` (Integer) — The nanos of the timestamp.

**Returns**
- `TimeStamp` — This time stamp object, for chaining.

### setSeconds(seconds)

`setSeconds(seconds: Integer): TimeStamp`

Sets the seconds of the timestamp, it represents the number of seconds since the Unix epoch (January 1, 1970, 00:00:00 UTC).

**Parameters**
- `seconds` (Integer) — The seconds of the timestamp.

**Returns**
- `TimeStamp` — This time stamp object, for chaining.

## Code Sample

```javascript
const timeStamp = AddOnsResponseService.newTimeStamp()
    .setSeconds(10086)
    .setNanos(123);
```
