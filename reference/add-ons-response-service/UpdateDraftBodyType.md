# UpdateDraftBodyType

An enum value that specifies the type of an `UpdateDraftBodyAction`.

An enum value that specifies the type of an `UpdateDraftBodyAction`.

To call an enum, use this pattern: `AddOnsResponseService.UpdateDraftBodyType.IN_PLACE_INSERT`.

## Properties

| Property | Description |
|----------|-------------|
| `IN_PLACE_INSERT` | Default. Update actions insert content at the current cursor position, replacing any selected content. |
| `INSERT_AT_START` | Update actions insert content at the start of message body. |
| `INSERT_AT_END` | Update actions insert content at the end of the message body. If an email signature is present, in Gmail on the web, the update action inserts after the user's signature. In the Gmail mobile app, the update action inserts before the user's signature. |
