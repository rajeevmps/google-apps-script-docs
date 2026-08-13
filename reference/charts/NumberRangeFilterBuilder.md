# NumberRangeFilterBuilder

A builder for number range filter controls.

A builder for number range filter controls. A number range filter is a slider with two thumbs that lets the user select ranges of numeric values. The control filters rows that don't match the selected range when applied to a number column.

## Methods

### setMaxValue(maxValue)

Returns: `NumberRangeFilterBuilder`

Sets the maximum allowed value for the range lower extent. If undefined, the value is inferred from the contents of the DataTable managed by the control.

**Parameters**

| Name | Type | Description |
|---|---|---|
| maxValue | Integer | the maximum allowed value |

### setMinValue(minValue)

Returns: `NumberRangeFilterBuilder`

Sets the minimum allowed value for the range lower extent. If undefined, the value is inferred from the contents of the DataTable managed by the control.

**Parameters**

| Name | Type | Description |
|---|---|---|
| minValue | Integer | the minimum allowed value |

### setOrientation(orientation)

Returns: `NumberRangeFilterBuilder`

Sets the slider orientation, to control whether the range filter displays horizontally or vertically.

**Parameters**

| Name | Type | Description |
|---|---|---|
| orientation | Orientation | the slider orientation |

### setShowRangeValues(showRangeValues)

Returns: `NumberRangeFilterBuilder`

Sets whether to have labels next to the slider displaying extents of the selected range for user visibility.

**Parameters**

| Name | Type | Description |
|---|---|---|
| showRangeValues | Boolean | whether to show range values |

### setTicks(ticks)

Returns: `NumberRangeFilterBuilder`

Sets the number of ticks (fixed positions in a range bar) a number range filter slider thumbs can fall in, to control slider precision.

**Parameters**

| Name | Type | Description |
|---|---|---|
| ticks | Integer | the number of ticks |

## Properties

None.
