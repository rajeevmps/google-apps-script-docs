# Role

Possible roles of a user within a group, such as owner or ordinary member.

A user has exactly one role within a group they are subscribed to. Roles in a group can be OWNER, MANAGER, MEMBER, INVITED, PENDING, or BANNED. To call an enum representing a role, use the format `GroupsApp.Role.ROLE_NAME`.

## Properties (Enum Values)

| Property | Description |
|----------|--------------|
| `OWNER` | The owner of a group. |
| `MANAGER` | The manager of a group. |
| `MEMBER` | A user who is a member of this group but is neither an owner nor a manager. |
| `INVITED` | A user who has been invited to join a group by an owner or manager but who has not yet accepted the invitation. |
| `PENDING` | A user who has requested to join a group but who has not yet been approved by an owner or manager. |
| `BANNED` | A user who has been banned from a group and cannot attempt to join it. |
