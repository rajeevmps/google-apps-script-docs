# ListStyle

Represents the list styling for a range of text.

ListStyle represents the list styling for a range of text. Methods enable applying list presets, retrieving glyph information, accessing parent lists, determining nesting levels, checking list membership, and removing text from lists.

## Methods

### applyListPreset(listPreset)

`ListStyle`

Applies the specified ListPreset to all paragraphs overlapping with the text. The nesting level of each paragraph is determined by counting leading tabs. Leading tabs are removed to avoid excess spacing between glyphs and paragraphs. If the immediately preceding paragraph is in a List with matching preset and current paragraphs are not in a different list, they may be added to that preceding list.

**Parameters**

- `listPreset` (`ListPreset`) — The list preset to apply.

**Returns**

`ListStyle` — This ListStyle for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getGlyph()

`String|null`

Returns the rendered glyph for the text. Returns null if the text spans more than one paragraph or is not in a list.

**Returns**

`String|null` — the rendered glyph, or null.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getList()

`List|null`

Returns the List the text is in, or null if none of the text is in a list, part of text is in a list, or text is in multiple lists. Call isInList() to determine whether text is in a list.

**Returns**

`List|null` — the list the text is in, or null.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getNestingLevel()

`Integer|null`

Returns the 0-based nesting level of the text. Returns null if the text is not in a list or mixed values exist.

**Returns**

`Integer|null` — the nesting level, or null.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### isInList()

`Boolean|null`

Returns true if text is in exactly one list, false if none is in a list, and null if only some text is in a list or text is in multiple lists.

**Returns**

`Boolean|null` — whether the text is in a list.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### removeFromList()

`ListStyle`

Removes paragraphs overlapping with the text from any lists. The nesting level of each paragraph is visually preserved by adding indent to the start of paragraphs.

**Returns**

`ListStyle` — This ListStyle for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

## Properties

None.
