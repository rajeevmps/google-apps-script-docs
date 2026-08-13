# EntryPointType

Enum that defines the types of entry points that can be created by a conferencing add-on.

Enum that defines the types of entry points that can be created by a conferencing add-on. Access via `ConferenceDataService.EntryPointType.[PROPERTY]`.

## Properties (Enum Values)

| Property | Description |
|----------|--------------|
| `VIDEO` | A video entry point for a conference. A conference can have zero or one `VIDEO` entry points. |
| `PHONE` | A phone entry point for a conference. A conference can have zero or more `PHONE` entry points. |
| `MORE` | A link to more information about entry points into a conference. A conference can have zero or one `MORE` entry points. A conference with only a `MORE` entry point is not valid. |
| `SIP` | A SIP entry point for a conference. A conference can have zero or one `SIP` entry points. |
