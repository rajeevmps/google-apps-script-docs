# YouTube Analytics Service

Source: https://developers.google.com/apps-script/advanced/youtube-analytics

## Overview

The YouTube Analytics service enables developers to access YouTube Analytics API capabilities within Google Apps Script. According to the documentation, this service allows you to "retrieve viewing statistics, popularity metrics, and demographic information for YouTube videos and channels."

## Key Requirements

This is classified as an **advanced service** that must be enabled before use. The service uses identical objects, methods, and parameters as the public YouTube Analytics API.

## Sample Implementation

The documentation provides a practical example that creates a spreadsheet with analytics data:

```javascript
/**
 * Creates a spreadsheet containing daily view counts, watch-time metrics,
 * and new-subscriber counts for a channel's videos.
 */
function createReport() {
  // Retrieve info about the user's YouTube channel.
  const channels = YouTube.Channels.list("id,contentDetails", {
    mine: true,
  });
  const channelId = channels.items[0].id;

  // Retrieve analytics report for the channel.
  const oneMonthInMillis = 1000 * 60 * 60 * 24 * 30;
  const today = new Date();
  const lastMonth = new Date(today.getTime() - oneMonthInMillis);

  const metrics = [
    "views",
    "estimatedMinutesWatched",
    "averageViewDuration",
    "subscribersGained",
  ];
  const result = YouTubeAnalytics.Reports.query({
    ids: `channel==${channelId}`,
    startDate: formatDateString(lastMonth),
    endDate: formatDateString(today),
    metrics: metrics.join(","),
    dimensions: "day",
    sort: "day",
  });

  if (!result.rows) {
    console.log("No rows returned.");
    return;
  }
  const spreadsheet = SpreadsheetApp.create("YouTube Analytics Report");
  const sheet = spreadsheet.getActiveSheet();

  // Append the headers.
  const headers = result.columnHeaders.map((columnHeader) => {
    return formatColumnName(columnHeader.name);
  });
  sheet.appendRow(headers);

  // Append the results.
  sheet
    .getRange(2, 1, result.rows.length, headers.length)
    .setValues(result.rows);

  console.log("Report spreadsheet created: %s", spreadsheet.getUrl());
}
```

## Helper Functions

```javascript
function formatDateString(date) {
  return Utilities.formatDate(date, Session.getScriptTimeZone(), "yyyy-MM-dd");
}

function formatColumnName(columnName) {
  let name = columnName.replace(/([a-z])([A-Z])/g, "$1 $2");
  name = name.slice(0, 1).toUpperCase() + name.slice(1);
  return name;
}
```

## API Versions

The example utilizes version 2 of the YouTube Analytics API and version 3 of the YouTube Data API.
</content>
