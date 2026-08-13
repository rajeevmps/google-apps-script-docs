# MatchType

An enumeration of how a string value should be matched.

An enumeration of how a string value should be matched. Matching a string is a boolean operation. Given a string, a match term (string), and a match type, the operation outputs `true` in the following cases:

1. If the match type equals EXACT and the match term equals the string.
2. If the match type equals PREFIX and the match term is a prefix of the string.
3. If the match type equals ANY and the match term is a substring of the string.

This enumeration can be used in by a string filter control to decide which rows to filter out of the data table.

## Methods

None.

## Properties

| Property | Type | Description |
|---|---|---|
| EXACT | Enum | Match exact values only |
| PREFIX | Enum | Match prefixes starting from the beginning of the value |
| ANY | Enum | Match any substring |
