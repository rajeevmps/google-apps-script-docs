# Admin SDK Google Workspace Reseller Service

Source: https://developers.google.com/apps-script/advanced/admin-sdk-reseller

## Overview

The Admin SDK Google Workspace Reseller service enables Apps Script developers to manage Google Workspace subscriptions through the Reseller API. According to the documentation, this service "lets you use the Admin SDK Reseller API in Google Apps Script" and "allows authorized reseller admins to place customer orders and manage Google Workspace monthly post-pay subscriptions."

## Enabling the Service

This is an advanced service that must be enabled before use. See the guide on [enabling advanced services](https://developers.google.com/apps-script/guides/services/advanced) for complete instructions.

## Key Characteristics

- Uses identical objects, methods, and parameters as the public Admin SDK Reseller API
- Requires reseller admin authorization
- Supports version 1 of the API
- Reference documentation available at the Admin SDK Reseller API reference guide (external — not scraped)

## Sample Code Example

```javascript
function getSubscriptions() {
  let result;
  let pageToken;
  do {
    result = AdminReseller.Subscriptions.list({
      pageToken: pageToken,
    });
    for (const sub of result.subscriptions) {
      const creationDate = new Date();
      creationDate.setUTCSeconds(sub.creationTime);
      console.log(
        "customer ID: %s, date created: %s, plan name: %s, sku id: %s",
        sub.customerId,
        creationDate.toDateString(),
        sub.plan.planName,
        sub.skuId,
      );
    }
    pageToken = result.nextPageToken;
  } while (pageToken);
}
```

This example demonstrates pagination through subscription results using page tokens.

## Support Resources

For issues and support, consult the Admin SDK Reseller support guide (external — not scraped).
</content>
