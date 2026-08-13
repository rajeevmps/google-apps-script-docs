# EntryPointFeature

Enum that defines the features of the entry point that can be created by a conferencing add-on.

Enum that defines the features of the entry point that can be created by a conferencing add-on. To reference this enum, use the pattern `ConferenceDataService.EntryPointFeature.[PROPERTY]`.

## Properties (Enum Values)

| Property | Description |
|----------|--------------|
| `UNKNOWN_FEATURE` | Do not use. Here only as a default value for compatibility reasons. |
| `TOLL` | Applies to PHONE entry point only. A call to a toll number is charged to the calling party. A number can't be toll and toll-free at the same time. |
| `TOLL_FREE` | Applies to PHONE entry point only. For the calling party, a call to a toll-free number is free of charge. A number can't be toll and toll-free at the same time. |
