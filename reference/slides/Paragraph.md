# Paragraph

A segment of text terminated by a newline character.

"A Paragraph is a segment of text terminated by a newline character."

The Paragraph class represents a text segment ending with a newline in Google Slides presentations. Key capabilities include retrieving the newline's position and accessing the text content within the paragraph.

## Methods

### getIndex()

`Integer|null`

Returns the index of the paragraph's newline. Returns `null` if the newline has been deleted.

**Returns**

`Integer|null` — the index of the paragraph's newline, or null if deleted.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getRange()

`TextRange|null`

Returns a `TextRange` spanning the text in the paragraph ended by this object's newline character. Returns `null` if the paragraph's newline has been deleted.

**Returns**

`TextRange|null` — the text range of the paragraph, or null if the newline has been deleted.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

## Properties

None.
