# DashStyle

The kinds of dashes with which linear geometry can be rendered.

The kinds of dashes with which linear geometry can be rendered. These values are based on the "ST_PresetLineDashVal" simple type described in section 20.1.10.48 of "Office Open XML File Formats - Fundamentals and Markup Language Reference," part 1 of ECMA-376 5th edition.

To access these values, use `SlidesApp.DashStyle.DOT`.

## Values

- `UNSUPPORTED` — A dash style that is not supported.
- `SOLID` — Solid line. Corresponds to ECMA-376 ST_PresetLineDashVal value 'solid'. This is the default dash style.
- `DOT` — Dotted line. Corresponds to ECMA-376 ST_PresetLineDashVal value 'dot'.
- `DASH` — Dashed line. Corresponds to ECMA-376 ST_PresetLineDashVal value 'dash'.
- `DASH_DOT` — Alternating dashes and dots. Corresponds to ECMA-376 ST_PresetLineDashVal value 'dashDot'.
- `LONG_DASH` — Line with large dashes. Corresponds to ECMA-376 ST_PresetLineDashVal value 'lgDash'.
- `LONG_DASH_DOT` — Alternating large dashes and dots. Corresponds to ECMA-376 ST_PresetLineDashVal value 'lgDashDot'.
