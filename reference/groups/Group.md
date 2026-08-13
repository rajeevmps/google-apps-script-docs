# Group

A group object whose members and roles can be queried.

A group object whose members and those members' roles within the group can be queried. This class allows retrieving a group's email address, direct child groups, and direct members. Users can check if specific users or groups are direct members and obtain their roles within the group.

## Methods

### getEmail()

**Signature:** `getEmail(): String`

**Returns:** `String`

**Description:** Gets this group's email address.

### getGroups()

**Signature:** `getGroups(): Group[]`

**Returns:** `Group[]`

**Description:** Retrieves the direct child groups of the group. Throws an exception if you do not have permission to view the group's member list.

### getRole(email)

**Signature:** `getRole(email: String): Role`

**Returns:** `Role`

**Description:** Retrieves a user's role in the context of the group. A user who is a direct member of a group has exactly one role within that group. Throws an exception if the user is not a member of the group or if you do not have permission to view the group's member list.

### getRole(user)

**Signature:** `getRole(user: User): Role`

**Returns:** `Role`

**Description:** Retrieves a user's role in the context of the group, accepting a User object instead of an email string. Same behavior as `getRole(email)`.

### getRoles(users)

**Signature:** `getRoles(users: User[]): Role[]`

**Returns:** `Role[]`

**Description:** Retrieves users' roles in the context of the group. A user who is a direct member of a group has exactly one role within that group. Throws an exception if any user is not a member of the group or if you do not have permission to view the group's member list.

### getUsers()

**Signature:** `getUsers(): User[]`

**Returns:** `User[]`

**Description:** Gets the direct members and banned members of the group that have a known corresponding Google account. Throws an exception if you don't have permission to view the group's member list or the member emails.

### hasGroup(group)

**Signature:** `hasGroup(group: Group): Boolean`

**Returns:** `Boolean`

**Description:** Tests if a group is a direct member of this group. The method does not return true if the tested group is nested more than one level below this group. Throws an exception if you do not have permission to view the group's member list.

### hasGroup(email)

**Signature:** `hasGroup(email: String): Boolean`

**Returns:** `Boolean`

**Description:** Tests if a group is a direct member of this group, identified by email address. Same behavior as `hasGroup(group)`.

### hasUser(email)

**Signature:** `hasUser(email: String): Boolean`

**Returns:** `Boolean`

**Description:** Tests if a user is a direct member of the group. Throws an exception if you do not have permission to view the group's member list.

### hasUser(user)

**Signature:** `hasUser(user: User): Boolean`

**Returns:** `Boolean`

**Description:** Tests if a user is a direct member of the group, accepting a User object instead of an email string. Same behavior as `hasUser(email)`.
