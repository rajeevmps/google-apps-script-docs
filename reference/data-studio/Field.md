# Field

Contains field-related data.

Contains field-related data. Its properties determine how the field is used in Data Studio. Fields can be created using methods like `fields.newDimension()` and support method chaining for configuration.

## Methods

### getAggregation()

**Signature:** `getAggregation(): AggregationType`

**Description:** Returns the `AggregationType` of this `Field`. `AggregationType` determines how Data Studio combines similar data into dimensions.

### getDescription()

**Signature:** `getDescription(): String`

**Description:** Returns the description of this `Field`. Descriptions are short explanations of a field's purpose.

### getFormula()

**Signature:** `getFormula(): String`

**Description:** Returns the formula of this `Field`. Formulas define a data transformation that Data Studio runs at query-time.

### getGroup()

**Signature:** `getGroup(): String`

**Description:** Returns the group of this `Field`. Fields collected into a group are presented together in the Data Studio UI.

### getId()

**Signature:** `getId(): String`

**Description:** Returns the ID of this `Field`. IDs are unique per set of fields and are used in formulas to refer to fields.

### getIsReaggregatable()

**Signature:** `getIsReaggregatable(): Boolean`

**Description:** Returns `true` if this field can be reaggregated, `false` otherwise.

### getName()

**Signature:** `getName(): String`

**Description:** Returns the name of this `Field`. Names are shown to the user to distinguish fields.

### getType()

**Signature:** `getType(): FieldType`

**Description:** Returns the `FieldType` of this `Field`.

### isDefault()

**Signature:** `isDefault(): Boolean`

**Description:** Returns `true` if this `Field` is the default metric or dimension.

### isDimension()

**Signature:** `isDimension(): Boolean`

**Description:** Returns `true` if this field is a dimension.

### isHidden()

**Signature:** `isHidden(): Boolean`

**Description:** Returns `true` if this `Field` is hidden. You can use hidden fields in formulas, but not in charts.

### isMetric()

**Signature:** `isMetric(): Boolean`

**Description:** Returns `true` if this field is a metric.

### setAggregation(aggregation)

**Signature:** `setAggregation(aggregation: AggregationType): Field`

**Description:** Sets the aggregation type of this `Field`. This throws an error if called on a metric.

### setDescription(description)

**Signature:** `setDescription(description: String): Field`

**Description:** Sets the description of this `Field`.

### setFormula(formula)

**Signature:** `setFormula(formula: String): Field`

**Description:** Sets the formula of this `Field`. Formulas define a data transformation that Data Studio runs at query-time.

### setGroup(group)

**Signature:** `setGroup(group: String): Field`

**Description:** Sets the group of this `Field`. Fields collected into a group are presented together in the Data Studio UI.

### setId(id)

**Signature:** `setId(id: String): Field`

**Description:** Sets the ID of this `Field`. IDs are unique per set of fields and are used in formulas to refer to fields.

### setIsHidden(isHidden)

**Signature:** `setIsHidden(isHidden: Boolean): Field`

**Description:** Sets the hidden status of this `Field`. You cannot hide fields containing formulas.

### setIsReaggregatable(isReaggregatable)

**Signature:** `setIsReaggregatable(isReaggregatable: Boolean): Field`

**Description:** Sets the reaggregation-permitted status for a `Field`. Attempting to set an aggregation type on a field that can't be reaggregated results in an error.

### setName(name)

**Signature:** `setName(name: String): Field`

**Description:** Sets the name of this `Field`. Names are shown to the user to distinguish fields.

### setType(type)

**Signature:** `setType(type: FieldType): Field`

**Description:** Sets the `FieldType` of this `Field`.
