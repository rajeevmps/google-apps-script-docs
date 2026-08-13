# DoubleClick Campaigns Service

Source: https://developers.google.com/apps-script/advanced/doubleclick-campaigns

Note: The slug `dfareporting` returned a 404. The live page is served at the `doubleclick-campaigns` slug; content below was fetched from that URL. This is the service for the DCM/DFA Reporting and Trafficking API (Campaign Manager 360).

## Overview

The DoubleClick Campaigns service in Apps Script enables programmatic access to DoubleClick Campaign Manager and DoubleClick Digital Marketing Reporting through the DCM/DFA Reporting and Trafficking API. This is an advanced service requiring explicit enablement before use.

## Key Information

**Service Type:** Advanced Service (must be enabled)

**API Reference:** Uses the same objects, methods, and parameters as the public [DCM/DFA Reporting and Trafficking API](https://developers.google.com/doubleclick-advertisers/rest/v4)

**Support:** For issues and assistance, consult the [DCM/DFA Reporting and Trafficking support guide](https://developers.google.com/doubleclick-advertisers/get-support)

## Sample Code

### List User Profiles

```javascript
/**
 * Logs all of the user profiles available in the account.
 */
function listUserProfiles() {
  try {
    const profiles = DoubleClickCampaigns.UserProfiles.list();

    if (profiles.items) {
      for (let i = 0; i < profiles.items.length; i++) {
        const profile = profiles.items[i];
        console.log(
          'Found profile with ID %s and name "%s".',
          profile.profileId,
          profile.userName,
        );
      }
    }
  } catch (e) {
    console.log("Failed with error: %s", e.error);
  }
}
```

### List Active Campaigns

```javascript
/**
 * Logs names and ID's of all active campaigns.
 * Note the use of paging tokens to retrieve the whole list.
 */
function listActiveCampaigns() {
  const profileId = "1234567"; // Replace with your profile ID.
  const fields = "nextPageToken,campaigns(id,name)";
  let result;
  let pageToken;
  try {
    do {
      result = DoubleClickCampaigns.Campaigns.list(profileId, {
        archived: false,
        fields: fields,
        pageToken: pageToken,
      });
      if (result.campaigns) {
        for (let i = 0; i < result.campaigns.length; i++) {
          const campaign = result.campaigns[i];
          console.log(
            'Found campaign with ID %s and name "%s".',
            campaign.id,
            campaign.name,
          );
        }
      }
      pageToken = result.nextPageToken;
    } while (pageToken);
  } catch (e) {
    console.log("Failed with error: %s", e.error);
  }
}
```

### Create Advertiser and Campaign

```javascript
/**
 * Creates a new advertiser, and creates a new campaign with that advertiser.
 * The campaign is set to last for one month.
 */
function createAdvertiserAndCampaign() {
  const profileId = "1234567"; // Replace with your profile ID.

  const advertiser = {
    name: "Example Advertiser",
    status: "APPROVED",
  };

  try {
    const advertiserId = DoubleClickCampaigns.Advertisers.insert(
      advertiser,
      profileId,
    ).id;

    const landingPage = {
      advertiserId: advertiserId,
      archived: false,
      name: "Example landing page",
      url: "https://www.google.com",
    };
    const landingPageId = DoubleClickCampaigns.AdvertiserLandingPages.insert(
      landingPage,
      profileId,
    ).id;

    const campaignStart = new Date();
    const campaignEnd = new Date();
    campaignEnd.setMonth(campaignEnd.getMonth() + 1);

    const campaign = {
      advertiserId: advertiserId,
      defaultLandingPageId: landingPageId,
      name: "Example campaign",
      startDate: Utilities.formatDate(campaignStart, "GMT", "yyyy-MM-dd"),
      endDate: Utilities.formatDate(campaignEnd, "GMT", "yyyy-MM-dd"),
    };
    DoubleClickCampaigns.Campaigns.insert(campaign, profileId);
  } catch (e) {
    console.log("Failed with error: %s", e.error);
  }
}
```
