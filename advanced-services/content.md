# Shopping Content Service

Source: https://developers.google.com/apps-script/advanced/shopping-content

Note: The slug `content` returned a 404. The live page is served at the `shopping-content` slug; content below was fetched from that URL. This is the service for the Google Content API for Shopping.

## Overview

The Shopping Content Service enables Google Apps Script users to interact with the Google Content API for Shopping. "The Shopping Content Service lets you use the Google Content API for Shopping in Google Apps Script."

This service allows developers to manage product listings and Merchant Center accounts programmatically. The service utilizes the same objects, methods, and parameters as the public Google Content API for Shopping.

## Key Features

- Upload and manage product listings
- Manage Merchant Center accounts
- Batch operations for multiple products
- Account-level tax and shipping configuration

## Enabling the Service

This is an advanced service in Apps Script and must be enabled before use.

## Sample Code Examples

### Insert a Single Product

```javascript
/**
 * Inserts a product into the products list. Logs the API response.
 */
function productInsert() {
  const merchantId = 123456; // Replace this with your Merchant Center ID.
  const productResource = {
    offerId: "book123",
    title: "A Tale of Two Cities",
    description: "A classic novel about the French Revolution",
    link: "http://my-book-shop.com/tale-of-two-cities.html",
    imageLink: "http://my-book-shop.com/tale-of-two-cities.jpg",
    contentLanguage: "en",
    targetCountry: "US",
    channel: "online",
    availability: "in stock",
    condition: "new",
    googleProductCategory: "Media > Books",
    productType: "Media > Books",
    gtin: "9780007350896",
    price: {
      value: "2.50",
      currency: "USD",
    },
    shipping: [
      {
        country: "US",
        service: "Standard shipping",
        price: {
          value: "0.99",
          currency: "USD",
        },
      },
    ],
    shippingWeight: {
      value: "2",
      unit: "pounds",
    },
  };

  try {
    response = ShoppingContent.Products.insert(productResource, merchantId);
    console.log(response);
  } catch (e) {
    console.log("Failed with error: $s", e.error);
  }
}
```

### List Products

```javascript
/**
 * Lists the products for a given merchant.
 */
function productList() {
  const merchantId = 123456; // Replace this with your Merchant Center ID.
  let pageToken;
  let pageNum = 1;
  const maxResults = 10;
  try {
    do {
      const products = ShoppingContent.Products.list(merchantId, {
        pageToken: pageToken,
        maxResults: maxResults,
      });
      console.log(`Page ${pageNum}`);
      if (products.resources) {
        for (let i = 0; i < products.resources.length; i++) {
          console.log(`Item [${i}] ==> ${products.resources[i]}`);
        }
      } else {
        console.log(`No more products in account ${merchantId}`);
      }
      pageToken = products.nextPageToken;
      pageNum++;
    } while (pageToken);
  } catch (e) {
    console.log("Failed with error: $s", e.error);
  }
}
```

### Batch Insert Products

```javascript
/**
 * Batch updates products. Logs the response.
 */
function custombatch(productResource1, productResource2, productResource3) {
  const merchantId = 123456; // Replace this with your Merchant Center ID.
  custombatchResource = {
    entries: [
      {
        batchId: 1,
        merchantId: merchantId,
        method: "insert",
        productId: "book124",
        product: productResource1,
      },
      {
        batchId: 2,
        merchantId: merchantId,
        method: "insert",
        productId: "book125",
        product: productResource2,
      },
      {
        batchId: 3,
        merchantId: merchantId,
        method: "insert",
        productId: "book126",
        product: productResource3,
      },
    ],
  };
  try {
    const response = ShoppingContent.Products.custombatch(custombatchResource);
    console.log(response);
  } catch (e) {
    console.log("Failed with error: $s", e.error);
  }
}
```

### Update Account-Level Taxes

```javascript
/**
 * Updates content account tax information.
 * Logs the API response.
 */
function updateAccountTax() {
  const merchantId = 123456;
  const accountId = 123456;

  try {
    const accounttax = ShoppingContent.Accounttax.get(merchantId, accountId);
    console.log(accounttax);

    const taxInfo = {
      accountId: accountId,
      rules: [
        {
          useGlobalRate: true,
          locationId: 21135,
          shippingTaxed: true,
          country: "US",
        },
        {
          ratePercent: 3,
          locationId: 21136,
          country: "US",
        },
        {
          ratePercent: 2,
          locationId: 21160,
          shippingTaxed: true,
          country: "US",
        },
      ],
    };

    console.log(
      ShoppingContent.Accounttax.update(taxInfo, merchantId, accountId),
    );
  } catch (e) {
    console.log("Failed with error: $s", e.error);
  }
}
```

## Resources

- [Google Content API for Shopping Reference Documentation](https://developers.google.com/shopping-content/v2/reference/v2)
- [API Support Guide](https://developers.google.com/shopping-content/support/contact-us)
- [GitHub Code Samples](https://github.com/googleworkspace/apps-script-samples/blob/main/advanced/shoppingContent.gs)
