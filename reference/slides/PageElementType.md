# PageElementType

An enum used to classify different types of page elements.

PageElementType is an enum used to classify different types of page elements. You access enum properties by calling its parent class, name, and property, such as `SlidesApp.PageElementType.SHAPE`.

`UNSUPPORTED` represents a page element that cannot be further classified.

## Values

- `UNSUPPORTED` — Represents a page element that is not supported and cannot be further classified.
- `SHAPE` — Represents a generic shape that does not have a more specific classification.
- `IMAGE` — Represents an image.
- `VIDEO` — Represents a video.
- `TABLE` — Represents a table.
- `GROUP` — Represents a collection of page elements joined as a single unit.
- `LINE` — Represents a line.
- `WORD_ART` — Represents word art.
- `SHEETS_CHART` — Represents a linked chart embedded from Google Sheets.
- `SPEAKER_SPOTLIGHT` — Represents a speaker spotlight.
