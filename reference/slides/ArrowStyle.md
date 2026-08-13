# ArrowStyle

The kinds of start and end forms with which linear geometry can be rendered.

The kinds of start and end forms with which linear geometry can be rendered. Some values correspond to the "ST_LineEndType" simple type from ECMA-376 5th edition standards.

To access these values, use `SlidesApp.ArrowStyle.PROPERTY_NAME` (e.g., `SlidesApp.ArrowStyle.FILL_ARROW`).

## Values

- `UNSUPPORTED` — An arrow style that is not supported.
- `NONE` — No arrow.
- `STEALTH_ARROW` — Arrow with notched back. Corresponds to ECMA-376 ST_LineEndType value 'stealth'.
- `FILL_ARROW` — Filled arrow. Corresponds to ECMA-376 ST_LineEndType value 'triangle'.
- `FILL_CIRCLE` — Filled circle. Corresponds to ECMA-376 ST_LineEndType value 'oval'.
- `FILL_SQUARE` — Filled square.
- `FILL_DIAMOND` — Filled diamond. Corresponds to ECMA-376 ST_LineEndType value 'diamond'.
- `OPEN_ARROW` — Hollow arrow.
- `OPEN_CIRCLE` — Hollow circle.
- `OPEN_SQUARE` — Hollow square.
- `OPEN_DIAMOND` — Hollow diamond.
