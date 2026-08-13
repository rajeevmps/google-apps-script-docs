# CompanyField

A company field in a Contact. (Deprecated)

**Deprecated.** Use the [People API advanced service](https://developers.google.com/apps-script/advanced/people) instead.

A company field in a Contact, holding the company name and job title associated with the contact.

## Methods

### deleteCompanyField()

**Signature:** `deleteCompanyField(): void`

**Description:** Deletes this company field.

### getCompanyName()

**Signature:** `getCompanyName(): String`

**Description:** Gets the company name for this field.

### getJobTitle()

**Signature:** `getJobTitle(): String`

**Description:** Gets the job title for this field.

### isPrimary()

**Signature:** `isPrimary(): Boolean`

**Description:** Gets whether this is the primary field value.

### setAsPrimary()

**Signature:** `setAsPrimary(): CompanyField`

**Description:** Sets this field to primary.

### setCompanyName(company)

**Signature:** `setCompanyName(company: String): CompanyField`

**Description:** Sets the company name for this field.

### setJobTitle(title)

**Signature:** `setJobTitle(title: String): CompanyField`

**Description:** Sets the job title for this field.
