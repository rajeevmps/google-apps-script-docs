# ConferenceDataBuilder

A builder for ConferenceData objects.

The `ConferenceDataBuilder` is used to create `ConferenceData` objects. It provides methods to construct and validate conference data with parameters, entry points, IDs, errors, and notes.

## Methods

### addConferenceParameter(conferenceParameter)

**Signature:** `addConferenceParameter(conferenceParameter: ConferenceParameter): ConferenceDataBuilder`

**Description:** Incorporates a `ConferenceParameter` into the `ConferenceData` being constructed. The system permits a maximum of 300 parameters per instance. Returns the builder for method chaining. Throws an error if the parameter is invalid or the limit is exceeded.

### addEntryPoint(entryPoint)

**Signature:** `addEntryPoint(entryPoint: EntryPoint): ConferenceDataBuilder`

**Description:** Incorporates an `EntryPoint` into the `ConferenceData` being constructed. The system permits a maximum of 300 entry points per instance. Returns the builder for method chaining. Throws an error if the entry point is invalid or the limit is exceeded.

### build()

**Signature:** `build(): ConferenceData`

**Description:** Finalizes and validates the constructed `ConferenceData` object. Throws an error if validation fails.

### setConferenceId(conferenceId)

**Signature:** `setConferenceId(conferenceId: String): ConferenceDataBuilder`

**Description:** Establishes the conference identifier for the data. The identifier cannot exceed 512 characters. Returns the builder for chaining. Throws an error if the provided value exceeds length constraints.

### setConferenceSolutionId(conferenceSolutionId)

**Signature:** `setConferenceSolutionId(conferenceSolutionId: String): ConferenceDataBuilder`

**Description:** Specifies the solution identifier as defined in the add-on manifest. This required field for Google Workspace add-ons populates the conference's name and icon URL values. Cannot exceed 512 characters. Returns the builder for chaining. Throws an error if the value exceeds length constraints.

### setError(conferenceError)

**Signature:** `setError(conferenceError: ConferenceError): ConferenceDataBuilder`

**Description:** Designates a `ConferenceError` to indicate unsuccessful conference creation. Returns the builder for chaining. Throws an error if the error object is invalid.

### setNotes(notes)

**Signature:** `setNotes(notes: String): ConferenceDataBuilder`

**Description:** Specifies supplementary information such as administrative instructions or legal notices. May contain HTML formatting. Cannot exceed 2048 characters. Returns the builder for chaining. Throws an error if the text exceeds length constraints.
