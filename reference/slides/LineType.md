# LineType

The kinds of lines.

LineType represents various line types derived from a subset of ST_ShapeType values in ECMA-376. The enum is derived from "Office Open XML File Formats - Fundamentals and Markup Language Reference," specifically section 20.1.10.55 of ECMA-376 5th edition.

To access these values, use `SlidesApp.LineType.PROPERTY_NAME`.

## Values

- `UNSUPPORTED` — A line type that is not supported.
- `STRAIGHT_CONNECTOR_1` — Straight connector 1 form. Corresponds to ECMA-376 ST_ShapeType 'straightConnector1'.
- `BENT_CONNECTOR_2` — Bent connector 2 form. Corresponds to ECMA-376 ST_ShapeType 'bentConnector2'.
- `BENT_CONNECTOR_3` — Bent connector 3 form. Corresponds to ECMA-376 ST_ShapeType 'bentConnector3'.
- `BENT_CONNECTOR_4` — Bent connector 4 form. Corresponds to ECMA-376 ST_ShapeType 'bentConnector4'.
- `BENT_CONNECTOR_5` — Bent connector 5 form. Corresponds to ECMA-376 ST_ShapeType 'bentConnector5'.
- `CURVED_CONNECTOR_2` — Curved connector 2 form. Corresponds to ECMA-376 ST_ShapeType 'curvedConnector2'.
- `CURVED_CONNECTOR_3` — Curved connector 3 form. Corresponds to ECMA-376 ST_ShapeType 'curvedConnector3'.
- `CURVED_CONNECTOR_4` — Curved connector 4 form. Corresponds to ECMA-376 ST_ShapeType 'curvedConnector4'.
- `CURVED_CONNECTOR_5` — Curved connector 5 form. Corresponds to ECMA-376 ST_ShapeType 'curvedConnector5'.
- `STRAIGHT_LINE` — Straight line. Corresponds to ECMA-376 ST_ShapeType 'line'. This line type is not a connector.
