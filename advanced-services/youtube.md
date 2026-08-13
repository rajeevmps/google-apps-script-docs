# YouTube Service

Source: https://developers.google.com/apps-script/advanced/youtube

## Overview

The YouTube service enables Apps Script developers to access the YouTube Data API and YouTube Live Streaming API for managing videos, playlists, channels, and live events. As an advanced service, it must be enabled before use.

## Key Features

According to the documentation: "This API gives users the ability to manage their videos, playlists, channels, and live events."

The service utilizes the same objects, methods, and parameters as the public YouTube API, making it straightforward for developers familiar with the REST API to implement programmatic solutions.

## Reference Documentation

- [YouTube Data API v3](https://developers.google.com/youtube/v3/docs) (external — not scraped)
- [YouTube Live Streaming API](https://developers.google.com/youtube/v3/live/docs) (external — not scraped)

## Code Samples

### Search Videos by Keyword

```javascript
function searchByKeyword() {
  try {
    const results = YouTube.Search.list("id,snippet", {
      q: "dogs",
      maxResults: 25,
    });
    if (results === null) {
      console.log("Unable to search videos");
      return;
    }
    for (const item of results.items) {
      console.log("[%s] Title: %s", item.id.videoId, item.snippet.title);
    }
  } catch (err) {
    console.log("Failed with an error %s", err.message);
  }
}
```

### Retrieve User Uploads

The sample fetches the user's channel, accesses the uploads playlist, iterates through videos, and handles pagination with `nextPageToken`.

### Subscribe to Channel

```javascript
function addSubscription() {
  const channelId = "UC_x5XG1OV2P6uZZ5FSM9Ttw";
  const resource = {
    snippet: {
      resourceId: {
        kind: "youtube#channel",
        channelId: channelId,
      },
    },
  };

  try {
    const response = YouTube.Subscriptions.insert(resource, "snippet");
    console.log(
      "Added subscription for channel title : %s",
      response.snippet.title,
    );
  } catch (e) {
    if (e.message.match("subscriptionDuplicate")) {
      console.log(`Cannot subscribe; already subscribed to channel: ${channelId}`);
    } else {
      console.log(`Error adding subscription: ${e.message}`);
    }
  }
}
```
</content>
