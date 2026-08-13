# ContactGroup

A ContactGroup is a group of contacts. (Deprecated)

**Deprecated.** Use the [People API advanced service](https://developers.google.com/apps-script/advanced/people) instead.

A ContactGroup is a group of contacts. All methods are deprecated and require authorization scope `https://www.google.com/m8/feeds`.

## Methods

### addContact(contact)

**Signature:** `addContact(contact: Contact): ContactGroup`

**Description:** Adds the given contact to this group. Example: creates a new contact and adds it to the "Work Friends" contact group.

### deleteGroup()

**Signature:** `deleteGroup(): void`

**Description:** Deletes this contact group. Deletes non-system groups only; system groups cannot be deleted. Example: retrieves a contact group named "Work Friends" and deletes it.

### getContacts()

**Signature:** `getContacts(): Contact[]`

**Description:** Gets all the contacts in this contact group. Example: retrieves all contacts in the group named "Work Friends".

### getGroupName()

**Signature:** `getGroupName(): String`

**Description:** Returns the name of this group.

### getId()

**Signature:** `getId(): String`

**Description:** Gets the id of this contact group. Example: retrieves a contact group and gets its id.

### getName()

**Signature:** `getName(): String`

**Description:** Gets the name of this contact group. Example: creates a new contact group and retrieves its name.

### isSystemGroup()

**Signature:** `isSystemGroup(): Boolean`

**Description:** Gets a boolean value to determine whether this contact group is a system group (undeletable) or not. System groups are a set of groups that are predefined in Google Contacts, such as "My Contacts", "Family", "Coworkers", etc. Example: checks whether two groups are system groups.

### removeContact(contact)

**Signature:** `removeContact(contact: Contact): ContactGroup`

**Description:** Removes the given contact from this group. Example: retrieves contacts and removes them from the "Work Friends" group.

### setGroupName(name)

**Signature:** `setGroupName(name: String): void`

**Description:** Sets the name of this group.

### setName(name)

**Signature:** `setName(name: String): ContactGroup`

**Description:** Sets the name of this contact group. Example: renames contact group from "Work Friends" to "Work Buddies".
