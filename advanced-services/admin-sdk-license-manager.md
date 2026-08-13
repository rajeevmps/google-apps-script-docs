# Admin SDK Enterprise License Manager Service

Source: https://developers.google.com/apps-script/advanced/admin-sdk-license-manager

## Overview

The Admin SDK Enterprise License Manager service in Apps Script enables domain administrators to manage user licenses programmatically. According to the documentation, this service "lets you use the Admin SDK Enterprise License Manager API in Google Apps Script" and "lets domain admins assign, update, retrieve, and delete user licenses."

## Enabling the Service

This is classified as an advanced service that "must be enabled before use." See the guide on [how to enable advanced services](https://developers.google.com/apps-script/guides/services/advanced).

## Key Capabilities

The service supports core license management operations:
- Listing license assignments for domain users
- Inserting new license assignments
- Updating existing assignments
- Deleting license assignments

## Code Examples

### Retrieving License Assignments

```javascript
function getLicenseAssignments() {
  const productId = "Google-Apps";
  const customerId = "example.com";
  let assignments = [];
  let pageToken = null;
  do {
    const response = AdminLicenseManager.LicenseAssignments.listForProduct(
      productId,
      customerId,
      {
        maxResults: 500,
        pageToken: pageToken,
      },
    );
    assignments = assignments.concat(response.items);
    pageToken = response.nextPageToken;
  } while (pageToken);
  for (const assignment of assignments) {
    console.log(
      "userId: %s, productId: %s, skuId: %s",
      assignment.userId,
      assignment.productId,
      assignment.skuId,
    );
  }
}
```

### Adding License Assignments

```javascript
function insertLicenseAssignment() {
  const productId = "Google-Apps";
  const skuId = "Google-Vault";
  const userId = "marty@hoverboard.net";
  try {
    const results = AdminLicenseManager.LicenseAssignments.insert(
      { userId: userId },
      productId,
      skuId,
    );
    console.log(results);
  } catch (e) {
    console.log("Failed with an error %s ", e.message);
  }
}
```

## Reference Resources

Complete API documentation is available at the [Admin SDK Enterprise License Manager reference](https://developers.google.com/admin-sdk/licensing/v1/reference), and support guidance can be found in the [support guide](https://developers.google.com/admin-sdk/licensing/support). (External links — not scraped.)
</content>
