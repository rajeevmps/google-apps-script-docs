# StringFilterBuilder

A builder for string filter controls.

A builder for string filter controls. A string filter is a simple text input field that lets the user filter data via string matching. Given a column of type string and matching options, this control filters out the rows that don't match the term that's in the input field.

## Methods

### setCaseSensitive(caseSensitive)

Returns: `StringFilterBuilder`

Sets whether matching should be case sensitive or not. Returns the builder for method chaining.

**Parameters**

| Name | Type | Description |
|---|---|---|
| caseSensitive | Boolean | `true` enables case-sensitive matching |

### setMatchType(matchType)

Returns: `StringFilterBuilder`

Sets whether the control should match exact values only, prefixes starting from the beginning of the value, or any substring. Returns the builder for method chaining.

**Parameters**

| Name | Type | Description |
|---|---|---|
| matchType | MatchType | the match type |

### setRealtimeTrigger(realtimeTrigger)

Returns: `StringFilterBuilder`

Sets whether the control should match any time a key is pressed or only when the input field "changes" (loss of focus or pressing the Enter key). Returns the builder for method chaining.

**Parameters**

| Name | Type | Description |
|---|---|---|
| realtimeTrigger | Boolean | `true` triggers events in real time |

## Properties

None.
