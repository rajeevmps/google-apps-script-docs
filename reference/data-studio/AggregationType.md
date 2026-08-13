# AggregationType

An enum that specifies aggregation types applicable to a Field object.

An enumeration in Google Apps Script that specifies aggregation types applicable to a `Field` object within Data Studio applications. Access enum values through the parent class: `DataStudioApp.AggregationType.AVG`.

## Properties (Enum Values)

| Property | Description |
|----------|--------------|
| `AVG` | Average. |
| `COUNT` | Count. |
| `COUNT_DISTINCT` | Count Distinct. |
| `MAX` | Max. |
| `MIN` | Min. |
| `SUM` | Sum. |
| `AUTO` | Auto. Use Auto for calculated fields which reference an aggregated field. |
| `NO_AGGREGATION` (Deprecated) | DEPRECATED: Use `AUTO` instead. No aggregation. |
