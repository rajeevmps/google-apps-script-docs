# GetDataResponse

Builder to create a getData() response for your script project.

Builder to create a `getData()` response for your script project. The class allows you to add rows of data and set fields, ultimately producing an object formatted for Data Studio consumption.

## Methods

### addAllRows(rows)

**Signature:** `addAllRows(rows: String[][]): GetDataResponse`

**Description:** Adds multiple rows of data to this `GetDataResponse`. Returns this builder, for chaining.

### addRow(row)

**Signature:** `addRow(row: String[]): GetDataResponse`

**Description:** Adds a row of data to this `GetDataResponse`. Returns this builder, for chaining.

### build()

**Signature:** `build(): Object`

**Description:** Validates this object and returns it in the format needed by Data Studio. Returns the validated `GetDataResponse` object.

### setFields(fields)

**Signature:** `setFields(fields: Fields): GetDataResponse`

**Description:** Sets the `Fields` of the builder. Returns this builder, for chaining.

### setFiltersApplied(filtersApplied)

**Signature:** `setFiltersApplied(filtersApplied: Boolean): GetDataResponse`

**Description:** Sets the filters applied status for this builder. Set to `true` if all filters were successfully applied, `false` otherwise. Returns this builder, for chaining.
