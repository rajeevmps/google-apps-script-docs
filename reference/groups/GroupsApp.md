# GroupsApp

Provides access to Google Groups information.

This class provides access to Google Groups information. It can be used to query information such as a group's email address, or the list of groups in which the user is a direct member.

## Methods

### getGroupByEmail(email)

**Signature:** `getGroupByEmail(email: String): Group`

**Returns:** `Group`

**Description:** Retrieves the group having the specified email address. Throws an exception if the group does not exist or if you do not have permission to see it.

**Authorization required:** `https://www.googleapis.com/auth/groups`

### getGroups()

**Signature:** `getGroups(): Group[]`

**Returns:** `Group[]`

**Description:** Retrieves all the groups of which you are a direct member (or a pending member). This is an empty list if you are not in any groups. Throws an exception if the group does not exist or if you do not have permission to see it.

Note that if you are a member of a group, B, which is itself a member of another group, A, then you are indirectly subscribed to group A. This method can be combined with `Group.getRole(email)` to determine membership status.

**Authorization required:** `https://www.googleapis.com/auth/groups`

## Code Samples

Two code examples are included on the reference page demonstrating basic usage of both methods: retrieving a group by email address and checking membership status using `hasUser()`, and retrieving the list of groups a user directly belongs to.
