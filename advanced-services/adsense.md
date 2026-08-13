# AdSense Service

Source: https://developers.google.com/apps-script/advanced/adsense

## Service Overview

The AdSense service in Apps Script provides access to the AdSense Management API, enabling developers to retrieve account structure information and generate performance reports for AdSense accounts.

## Key Characteristics

**Access Level:** This is an advanced service requiring explicit enablement before use.

**API Version:** The documentation references version 2 of the AdSense Management API.

**Reference Documentation:** Complete details are available at the [AdSense Management API reference](https://developers.google.com/adsense/management/reference/rest).

**Support:** Issues and questions can be directed to Stack Overflow using the `adsense-api` tag.

## Code Samples

### 1. List Accounts

```javascript
/**
 * Lists available AdSense accounts.
 */
function listAccounts() {
  let pageToken;
  do {
    const response = AdSense.Accounts.list({ pageToken: pageToken });
    if (!response.accounts) {
      console.log("No accounts found.");
      return;
    }
    for (const account of response.accounts) {
      console.log(
        'Found account with resource name "%s" and display name "%s".',
        account.name,
        account.displayName,
      );
    }
    pageToken = response.nextPageToken;
  } while (pageToken);
}
```

### 2. List Ad Clients

```javascript
/**
 * Logs available Ad clients for an account.
 *
 * @param {string} accountName The resource name of the account that owns the
 *     collection of ad clients.
 */
function listAdClients(accountName) {
  let pageToken;
  do {
    const response = AdSense.Accounts.Adclients.list(accountName, {
      pageToken: pageToken,
    });
    if (!response.adClients) {
      console.log("No ad clients found for this account.");
      return;
    }
    for (const adClient of response.adClients) {
      console.log(
        'Found ad client for product "%s" with resource name "%s".',
        adClient.productCode,
        adClient.name,
      );
      console.log(
        "Reporting dimension ID: %s",
        adClient.reportingDimensionId ?? "None",
      );
    }
    pageToken = response.nextPageToken;
  } while (pageToken);
}
```

### 3. List Ad Units

```javascript
/**
 * Lists ad units.
 * @param {string} adClientName The resource name of the ad client that owns the collection
 *     of ad units.
 */
function listAdUnits(adClientName) {
  let pageToken;
  do {
    const response = AdSense.Accounts.Adclients.Adunits.list(adClientName, {
      pageSize: 50,
      pageToken: pageToken,
    });
    if (!response.adUnits) {
      console.log("No ad units found for this ad client.");
      return;
    }
    for (const adUnit of response.adUnits) {
      console.log(
        'Found ad unit with resource name "%s" and display name "%s".',
        adUnit.name,
        adUnit.displayName,
      );
    }

    pageToken = response.nextPageToken;
  } while (pageToken);
}
```

### 4. Generate a Report

```javascript
/**
 * Generates a spreadsheet report for a specific ad client in an account.
 * @param {string} accountName The resource name of the account.
 * @param {string} adClientReportingDimensionId The reporting dimension ID
 *     of the ad client.
 */
function generateReport(accountName, adClientReportingDimensionId) {
  // Prepare report.
  const today = new Date();
  const oneWeekAgo = new Date(today.getTime() - 7 * 24 * 60 * 60 * 1000);

  const report = AdSense.Accounts.Reports.generate(accountName, {
    // Specify the desired ad client using a filter.
    filters: [
      `AD_CLIENT_ID==${escapeFilterParameter(adClientReportingDimensionId)}`,
    ],
    metrics: [
      "PAGE_VIEWS",
      "AD_REQUESTS",
      "AD_REQUESTS_COVERAGE",
      "CLICKS",
      "AD_REQUESTS_CTR",
      "COST_PER_CLICK",
      "AD_REQUESTS_RPM",
      "ESTIMATED_EARNINGS",
    ],
    dimensions: ["DATE"],
    ...dateToJson("startDate", oneWeekAgo),
    ...dateToJson("endDate", today),
    // Sort by ascending date.
    orderBy: ["+DATE"],
  });

  if (!report.rows) {
    console.log("No rows returned.");
    return;
  }
  const spreadsheet = SpreadsheetApp.create("AdSense Report");
  const sheet = spreadsheet.getActiveSheet();

  // Append the headers.
  sheet.appendRow(report.headers.map((header) => header.name));

  // Append the results.
  sheet
    .getRange(2, 1, report.rows.length, report.headers.length)
    .setValues(report.rows.map((row) => row.cells.map((cell) => cell.value)));

  console.log("Report spreadsheet created: %s", spreadsheet.getUrl());
}

/**
 * Escape special characters for a parameter being used in a filter.
 * @param {string} parameter The parameter to be escaped.
 * @return {string} The escaped parameter.
 */
function escapeFilterParameter(parameter) {
  return parameter.replace("\\", "\\\\").replace(",", "\\,");
}

/**
 * Returns the JSON representation of a Date object (as a google.type.Date).
 *
 * @param {string} paramName the name of the date parameter
 * @param {Date} value the date
 * @return {object} formatted date
 */
function dateToJson(paramName, value) {
  return {
    [`${paramName}.year`]: value.getFullYear(),
    [`${paramName}.month`]: value.getMonth() + 1,
    [`${paramName}.day`]: value.getDate(),
  };
}
```

All samples are available on [GitHub](https://github.com/googleworkspace/apps-script-samples/blob/main/advanced/adsense.gs).
