# BigQueryConfig

A configuration object for a native BigQuery connector.

A configuration object for a native BigQuery connector. Return this object from `getData()` for Data Studio to query BigQuery for the connector.

## Methods

### addQueryParameter(name, type, value)

**Signature:** `addQueryParameter(name: String, type: BigQueryParameterType, value: String): BigQueryConfig`

**Description:** Adds a query parameter to this `BigQueryConfig`. Returns this object, for chaining.

### build()

**Signature:** `build(): Object`

**Description:** Validates this object and returns it in the format needed by Data Studio.

### printJson()

**Signature:** `printJson(): String`

**Description:** Prints the JSON representation of this object. This is for debugging only.

### setAccessToken(accessToken)

**Signature:** `setAccessToken(accessToken: String): BigQueryConfig`

**Description:** Sets the access token of this `BigQueryConfig`. Returns this object, for chaining.

### setBillingProjectId(billingProjectId)

**Signature:** `setBillingProjectId(billingProjectId: String): BigQueryConfig`

**Description:** Sets the billing project ID of this `BigQueryConfig`. Returns this object, for chaining.

### setQuery(query)

**Signature:** `setQuery(query: String): BigQueryConfig`

**Description:** Sets the SQL query of this `BigQueryConfig`. Returns this object, for chaining.

### setUseStandardSql(useStandardSql)

**Signature:** `setUseStandardSql(useStandardSql: Boolean): BigQueryConfig`

**Description:** Determines if the query is interpreted as standard or legacy SQL. If true, interpreted as standard SQL; if false, as legacy SQL. Returns this object, for chaining.
