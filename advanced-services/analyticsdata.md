# Analytics Data Service

Source: https://developers.google.com/apps-script/advanced/analyticsdata
(Note: `https://developers.google.com/apps-script/advanced/analytics` canonicalizes/redirects to this same page — there is no separate legacy "Analytics" advanced service page; both slugs serve this content.)

## Overview

The Analytics Data service enables Google Analytics users to access Google Analytics 4 (GA4) report data programmatically through the Google Analytics Data API v1 within Apps Script.

**Key characteristics:**
- "The Analytics Data service lets you use the Google Analytics Data API v1 in Google Apps Script"
- Must be enabled as an advanced service before use
- Uses identical objects, methods, and parameters as the public API

## Enabling the Service

This qualifies as an advanced service requiring activation before implementation in Apps Script.

## Reference Documentation

Detailed specifications are available through the [Google Analytics Data API v1 reference documentation](https://developers.google.com/analytics/devguides/reporting/data/v1/rest) (external — not scraped). For implementation guidance, see the support page at [Google Analytics Data API v1 help](https://developers.google.com/analytics/devguides/reporting/data/v1/help) (external — not scraped).

## Sample Implementation

The provided example demonstrates running a GA4 report that retrieves active user counts by geographic location and exports results to a spreadsheet:

```javascript
/**
 * Runs a report of a Google Analytics 4 property ID. Creates a sheet with the
 * report.
 */
function runReport() {
  const propertyId = "YOUR-GA4-PROPERTY-ID";

  try {
    const metric = AnalyticsData.newMetric();
    metric.name = "activeUsers";

    const dimension = AnalyticsData.newDimension();
    dimension.name = "city";

    const dateRange = AnalyticsData.newDateRange();
    dateRange.startDate = "2020-03-31";
    dateRange.endDate = "today";

    const request = AnalyticsData.newRunReportRequest();
    request.dimensions = [dimension];
    request.metrics = [metric];
    request.dateRanges = dateRange;

    const report = AnalyticsData.Properties.runReport(
      request,
      `properties/${propertyId}`,
    );

    if (!report.rows) {
      console.log("No rows returned.");
      return;
    }

    const spreadsheet = SpreadsheetApp.create("Google Analytics Report");
    const sheet = spreadsheet.getActiveSheet();

    const dimensionHeaders = report.dimensionHeaders.map((dimensionHeader) => {
      return dimensionHeader.name;
    });
    const metricHeaders = report.metricHeaders.map((metricHeader) => {
      return metricHeader.name;
    });
    const headers = [...dimensionHeaders, ...metricHeaders];

    sheet.appendRow(headers);

    const rows = report.rows.map((row) => {
      const dimensionValues = row.dimensionValues.map((dimensionValue) => {
        return dimensionValue.value;
      });
      const metricValues = row.metricValues.map((metricValues) => {
        return metricValues.value;
      });
      return [...dimensionValues, ...metricValues];
    });

    sheet.getRange(2, 1, report.rows.length, headers.length).setValues(rows);

    console.log("Report spreadsheet created: %s", spreadsheet.getUrl());
  } catch (e) {
    console.log("Failed with error: %s", e.error);
  }
}
```
</content>
