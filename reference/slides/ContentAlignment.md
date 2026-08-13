# ContentAlignment

The content alignments for a Shape or TableCell.

The content alignments for a `Shape` or `TableCell`. The supported alignments correspond to predefined text anchoring types from the ECMA-376 standard.

More information on these alignments can be found in the "ST_TextAnchoringType" simple type description in section 20.1.10.59 of "Office Open XML File Formats - Fundamentals and Markup Language Reference," part 1 of ECMA-376 5th edition.

To access these values, use `SlidesApp.ContentAlignment.PROPERTY_NAME`.

## Values

- `UNSUPPORTED` — A content alignment that is not supported.
- `TOP` — Aligns the content to the top of the content holder. Corresponds to ECMA-376 ST_TextAnchoringType 't'.
- `MIDDLE` — Aligns the content to the middle of the content holder. Corresponds to ECMA-376 ST_TextAnchoringType 'ctr'.
- `BOTTOM` — Aligns the content to the bottom of the content holder. Corresponds to ECMA-376 ST_TextAnchoringType 'b'.
