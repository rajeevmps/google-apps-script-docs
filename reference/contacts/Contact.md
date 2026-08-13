# Contact

A Contact contains the name, address, and various contact details of a contact. (Deprecated)

**Deprecated.** Use the [People API advanced service](https://developers.google.com/apps-script/advanced/people) instead.

A Contact contains the name, address, and various contact details of a contact. All methods described, including those for getting and setting various contact details like names, addresses, phone numbers, URLs, and user-defined fields, are marked as deprecated and should not be used in new scripts. These deprecated methods require authorization with the `https://www.google.com/m8/feeds` scope to function.

## Methods

### addAddress(label, address)

**Signature:** `addAddress(label: Object, address: String): AddressField`

**Description:** Adds an address to the contact with either a standard or custom label. The label can be either from ContactsApp.Field or a custom label string.

### addCompany(company, title)

**Signature:** `addCompany(company: String, title: String): CompanyField`

**Description:** Adds a company to the contact.

### addCustomField(label, content)

**Signature:** `addCustomField(label: Object, content: Object): CustomField`

**Description:** Adds a custom field to the contact with either an extended or custom label. The label can be either from ContactsApp.ExtendedField or a custom label string.

### addDate(label, month, day, year)

**Signature:** `addDate(label: Object, month: Month, day: Integer, year: Integer): DateField`

**Description:** Adds a date to the contact with either a standard or custom label. The label can be either from ContactsApp.Field or a custom label string.

### addEmail(label, address)

**Signature:** `addEmail(label: Object, address: String): EmailField`

**Description:** Add an email address with a standard label (home, work, etc.) or a custom label.

### addIM(label, address)

**Signature:** `addIM(label: Object, address: String): IMField`

**Description:** Adds an IM address to the contact with either a standard or custom label. The label can be either from ContactsApp.Field or a custom label string.

### addPhone(label, number)

**Signature:** `addPhone(label: Object, number: String): PhoneField`

**Description:** Adds a phone number to the contact with either a standard or custom label. The label can be either from ContactsApp.Field or a custom label string.

### addToGroup(group)

**Signature:** `addToGroup(group: ContactGroup): Contact`

**Description:** Adds this contact to the given contact group.

### addUrl(label, url)

**Signature:** `addUrl(label: Object, url: String): UrlField`

**Description:** Adds a URL to the contact with either a standard or custom label. The label can be either from ContactsApp.Field or a custom label string.

### deleteContact()

**Signature:** `deleteContact(): void`

**Description:** Deletes this contact.

### getAddresses()

**Signature:** `getAddresses(): AddressField[]`

**Description:** Gets all the addresses for this contact.

### getAddresses(label)

**Signature:** `getAddresses(label: Object): AddressField[]`

**Description:** Gets all the addresses for this contact matching a particular field. The label can be either from ContactsApp.Field or a custom label string.

### getCompanies()

**Signature:** `getCompanies(): CompanyField[]`

**Description:** Gets all the companies for this contact.

### getContactGroups()

**Signature:** `getContactGroups(): ContactGroup[]`

**Description:** Gets all the contact groups that contain this contact.

### getCustomFields()

**Signature:** `getCustomFields(): CustomField[]`

**Description:** Gets all the custom fields for this contact.

### getCustomFields(label)

**Signature:** `getCustomFields(label: Object): CustomField[]`

**Description:** Gets all the custom fields for this contact matching a particular field.

### getDates()

**Signature:** `getDates(): DateField[]`

**Description:** Gets all the dates for this contact.

### getDates(label)

**Signature:** `getDates(label: Object): DateField[]`

**Description:** Gets all the dates for this contact matching a particular field.

### getEmailAddresses()

**Signature:** `getEmailAddresses(): String[]`

**Description:** Gets a list of the email addresses available for this Contact.

### getEmails()

**Signature:** `getEmails(): EmailField[]`

**Description:** Gets the email addresses of this contact.

### getEmails(label)

**Signature:** `getEmails(label: Object): EmailField[]`

**Description:** Gets the email addresses for this contact matching a particular field.

### getFamilyName()

**Signature:** `getFamilyName(): String`

**Description:** Gets the family name (last name) of the contact as a string.

### getFullName()

**Signature:** `getFullName(): String`

**Description:** Gets the full name (given name and last name) of the contact as a string.

### getGivenName()

**Signature:** `getGivenName(): String`

**Description:** Gets the given name (first name) of the contact as a string.

### getHomeAddress()

**Signature:** `getHomeAddress(): String`

**Description:** Gets the home address of this Contact, or empty string if none exists.

### getHomeFax()

**Signature:** `getHomeFax(): String`

**Description:** Gets the home fax number of this Contact or empty string if none exists.

### getHomePhone()

**Signature:** `getHomePhone(): String`

**Description:** Gets the home phone number of this Contact or empty string if none exists.

### getIMs()

**Signature:** `getIMs(): IMField[]`

**Description:** Gets all the IM addresses for this contact.

### getIMs(label)

**Signature:** `getIMs(label: Object): IMField[]`

**Description:** Gets all the IM addresses for this contact matching a particular field.

### getId()

**Signature:** `getId(): String`

**Description:** Returns the unique id of this contact.

### getInitials()

**Signature:** `getInitials(): String`

**Description:** Gets the contact's initials.

### getLastUpdated()

**Signature:** `getLastUpdated(): Date`

**Description:** Gets the date this contact was last updated.

### getMaidenName()

**Signature:** `getMaidenName(): String`

**Description:** Gets the maiden name of the contact as a string.

### getMiddleName()

**Signature:** `getMiddleName(): String`

**Description:** Gets the middle name of the contact as a string.

### getMobilePhone()

**Signature:** `getMobilePhone(): String`

**Description:** Gets the mobile phone number of this Contact or empty string if none exists.

### getNickname()

**Signature:** `getNickname(): String`

**Description:** Gets the nickname of the contact as a string.

### getNotes()

**Signature:** `getNotes(): String`

**Description:** Gets the notes associated with this contact, or an empty string if there are no notes.

### getPager()

**Signature:** `getPager(): String`

**Description:** Gets the pager phone number of this Contact or empty string if none exists.

### getPhones()

**Signature:** `getPhones(): PhoneField[]`

**Description:** Gets all the phone numbers for this contact.

### getPhones(label)

**Signature:** `getPhones(label: Object): PhoneField[]`

**Description:** Gets all the phone numbers for this contact matching a particular field.

### getPrefix()

**Signature:** `getPrefix(): String`

**Description:** Gets the prefix to the contact's name.

### getPrimaryEmail()

**Signature:** `getPrimaryEmail(): String`

**Description:** Gets the primary email address of the contact as a string.

### getShortName()

**Signature:** `getShortName(): String`

**Description:** Gets the short name of the contact as a string.

### getSuffix()

**Signature:** `getSuffix(): String`

**Description:** Gets the suffix to the contact's name.

### getUrls()

**Signature:** `getUrls(): UrlField[]`

**Description:** Gets all the URLs for this contact.

### getUrls(label)

**Signature:** `getUrls(label: Object): UrlField[]`

**Description:** Gets all the URLs for this contact matching a particular field.

### getUserDefinedField(key)

**Signature:** `getUserDefinedField(key: String): String`

**Description:** Gets the user defined value associated with the given key.

### getUserDefinedFields()

**Signature:** `getUserDefinedFields(): Object`

**Description:** Gets all the user defined fields for this Contact and returns them as the properties of a JavaScript Object.

### getWorkAddress()

**Signature:** `getWorkAddress(): String`

**Description:** Gets the work address of this Contact, or empty string if none exists.

### getWorkFax()

**Signature:** `getWorkFax(): String`

**Description:** Gets the work fax number of this Contact or empty string if none exists.

### getWorkPhone()

**Signature:** `getWorkPhone(): String`

**Description:** Gets the work phone number of this Contact or empty string if none exists.

### removeFromGroup(group)

**Signature:** `removeFromGroup(group: ContactGroup): Contact`

**Description:** Removes this contact from the given contact group.

### setFamilyName(familyName)

**Signature:** `setFamilyName(familyName: String): Contact`

**Description:** Sets the family name (last name) of the contact.

### setFullName(fullName)

**Signature:** `setFullName(fullName: String): Contact`

**Description:** Sets the full name (given name and last name) of the contact.

### setGivenName(givenName)

**Signature:** `setGivenName(givenName: String): Contact`

**Description:** Sets the given name (first name) of the contact.

### setHomeAddress(addr)

**Signature:** `setHomeAddress(addr: String): void`

**Description:** Sets the home address of this Contact.

### setHomeFax(phone)

**Signature:** `setHomeFax(phone: String): void`

**Description:** Sets the home fax number of this Contact.

### setHomePhone(phone)

**Signature:** `setHomePhone(phone: String): void`

**Description:** Sets the home phone number of this Contact.

### setInitials(initials)

**Signature:** `setInitials(initials: String): Contact`

**Description:** Sets the contact's initials.

### setMaidenName(maidenName)

**Signature:** `setMaidenName(maidenName: String): Contact`

**Description:** Sets the maiden name of the contact.

### setMiddleName(middleName)

**Signature:** `setMiddleName(middleName: String): Contact`

**Description:** Sets the middle name of the contact.

### setMobilePhone(phone)

**Signature:** `setMobilePhone(phone: String): void`

**Description:** Sets the mobile phone number of this Contact.

### setNickname(nickname)

**Signature:** `setNickname(nickname: String): Contact`

**Description:** Sets the nickname of the contact.

### setNotes(notes)

**Signature:** `setNotes(notes: String): Contact`

**Description:** Sets the notes associated with this contact.

### setPager(phone)

**Signature:** `setPager(phone: String): void`

**Description:** Sets the pager number of this Contact.

### setPrefix(prefix)

**Signature:** `setPrefix(prefix: String): Contact`

**Description:** Sets the prefix to the contact's name.

### setPrimaryEmail(primaryEmail)

**Signature:** `setPrimaryEmail(primaryEmail: String): void`

**Description:** Sets the primary email address of this Contact.

### setShortName(shortName)

**Signature:** `setShortName(shortName: String): Contact`

**Description:** Sets the short name of the contact.

### setSuffix(suffix)

**Signature:** `setSuffix(suffix: String): Contact`

**Description:** Sets the suffix to the contact's name.

### setUserDefinedField(key, value)

**Signature:** `setUserDefinedField(key: String, value: String): void`

**Description:** Sets a single user defined field for this Contact, to be stored with a given key.

### setUserDefinedFields(o)

**Signature:** `setUserDefinedFields(o: Object): void`

**Description:** Sets the user defined fields for this Contact with the properties of the given Object.

### setWorkAddress(addr)

**Signature:** `setWorkAddress(addr: String): void`

**Description:** Sets the work address of this Contact.

### setWorkFax(phone)

**Signature:** `setWorkFax(phone: String): void`

**Description:** Sets the work fax number of this Contact.

### setWorkPhone(phone)

**Signature:** `setWorkPhone(phone: String): void`

**Description:** Sets the work phone number of this Contact.
