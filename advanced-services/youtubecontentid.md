# YouTube Content ID Service

Source: https://developers.google.com/apps-script/advanced/youtube-content-id

Note: The slug `youtubecontentid` (no hyphens) returned a 404. The live page is served at the `youtube-content-id` slug; content below was fetched from that URL.

## Overview

The YouTube Content ID service enables developers to interact with YouTube's rights management system through Apps Script. This advanced service integrates the YouTube Content ID API, allowing YouTube content partners to manage assets, claims, and campaigns programmatically.

**Important**: This service is restricted to YouTube content partners and may not be available to all developers. Access requires enrollment in the YouTube Partner Program.

## Key Capabilities

According to the documentation, developers can:
- "Create and manage your assets, claims and campaigns" as YouTube partners
- Interact directly with YouTube's Content ID rights management system
- Perform operations like claiming videos, updating asset ownership, and releasing claims

## Enabling the Service

This is an advanced service requiring enablement before use through the Google Developers Console.

## Sample Code Examples

### Claim a Video with Monetization Policy

```javascript
/**
 * Creates a partner-uploaded claim on a video with specified
 * asset and policy rules.
 */
function claimYourVideoWithMonetizePolicy() {
  const onBehalfOfContentOwner = "replaceWithYourContentOwnerID";
  const videoId = "replaceWithYourVideoID";
  const assetId = "replaceWithYourAssetID";
  const claimToInsert = {
    videoId: videoId,
    assetId: assetId,
    contentType: "audiovisual",
    policy: { rules: [{ action: "monetize" }] },
  };
  try {
    const claimInserted = YouTubeContentId.Claims.insert(claimToInsert, {
      onBehalfOfContentOwner: onBehalfOfContentOwner,
    });
    console.log("Claim created on video %s: %s", videoId, claimInserted);
  } catch (e) {
    console.log(
      "Failed to create claim on video %s, error: %s",
      videoId,
      e.message,
    );
  }
}
```

### Update Asset Ownership

```javascript
/**
 * Updates content owner's ownership on an existing asset.
 */
function updateAssetOwnership() {
  const onBehalfOfContentOwner = "replaceWithYourContentOwnerID";
  const assetId = "replaceWithYourAssetID";
  const myAssetOwnership = {
    general: [
      {
        ratio: 100,
        owner: onBehalfOfContentOwner,
        type: "include",
        territories: ["US", "CA"],
      },
    ],
  };
  try {
    const updatedOwnership = YouTubeContentId.Ownership.update(
      myAssetOwnership,
      assetId,
      { onBehalfOfContentOwner: onBehalfOfContentOwner },
    );
    console.log("Ownership updated on asset %s: %s", assetId, updatedOwnership);
  } catch (e) {
    console.log(
      "Ownership update failed on asset %s, error: %s",
      assetId,
      e.message,
    );
  }
}
```

### Release a Claim

```javascript
/**
 * Releases an existing claim on a video by changing status to inactive.
 */
function releaseClaim() {
  const onBehalfOfContentOwner = "replaceWithYourContentOwnerID";
  const claimId = "replaceWithYourClaimID";
  const claimToBeReleased = {
    status: "inactive",
  };
  try {
    const claimReleased = YouTubeContentId.Claims.patch(
      claimToBeReleased,
      claimId,
      { onBehalfOfContentOwner: onBehalfOfContentOwner },
    );
    console.log("Claim %s was released: %s", claimId, claimReleased);
  } catch (e) {
    console.log("Failed to release claim %s, error: %s", claimId, e.message);
  }
}
```

## Additional Resources

- Full API reference: [YouTube Content ID API v1 Documentation](https://developers.google.com/youtube/partner/docs/v1)
- Support: [YouTube API Support Guide](https://developers.google.com/youtube/v3/support)
- Sample code repository: [Google Workspace Apps Script Samples](https://github.com/googleworkspace/apps-script-samples)
