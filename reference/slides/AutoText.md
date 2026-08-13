# AutoText

An element of text that is dynamically replaced with content that can change over time, such as a slide number.

An element of text that is dynamically replaced with content that can change over time, such as a slide number.

## Methods

### getAutoTextType()

`AutoTextType`

Returns the type of auto text. Returns `null` if the auto text has been deleted.

**Returns**

`AutoTextType` — the type of the auto text, or `null` if the auto text has been deleted

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getIndex()

`Integer`

Returns the index of the auto text. Returns `null` if the auto text has been deleted.

**Returns**

`Integer` — the index of the auto text, or `null` if the auto text has been deleted

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getRange()

`TextRange`

Returns a `TextRange` spanning the auto text. Returns `null` if the auto text has been deleted.

**Returns**

`TextRange` — a text range spanning the auto text, or `null` if the auto text has been deleted

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`
