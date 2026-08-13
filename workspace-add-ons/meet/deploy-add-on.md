# Deploy a Meet add-on

## Create a Google Cloud project

To generate a Google Cloud project, see [Create a Google Cloud project](/workspace/guides/create-project).

## Enable the Google Workspace Marketplace SDK and Google Workspace add-ons API

The Marketplace SDK and Google Workspace add-ons API are required to develop Meet add-ons. To enable them:

1. Open the [Google Cloud console](https://console.cloud.google.com/).
2. At the top, if a different project is already open, select the project name of your app's project to switch projects.
3. At the top, in the search bar, type `Google Workspace Marketplace SDK` and press enter.
4. Open the `Google Workspace Marketplace SDK` page, click **Enable**.

**Warning:** Make sure you enable the `Google Workspace Marketplace SDK`, not the API. The `Google Workspace Marketplace API` is a different tool used to integrate with Google's licensing and billing services.

5. Repeat these steps to find and enable the `Google Workspace add-ons API`.

## Create a deployment

To use an add-on in Meet, you need a deployment and an [add-on manifest file](/apps-script/add-ons/concepts/workspace-manifests).

### Navigate to the Google Workspace Marketplace SDK for your project in Google Cloud console

1. Open the [Google Cloud console](https://console.cloud.google.com/).
2. At the top, if a different project is already open, select the project name of your app's project to switch projects.
3. Click **APIs & Services**.
4. Select `Google Workspace Marketplace SDK` to view the details page.

### Create your deployment

You can create your deployment directly in Google Cloud console by creating an HTTP deployment (recommended), or by using Google Apps Script.

### HTTP deployment

1. Click the **HTTP deployments** tab.
2. Click **Create new deployment** and enter the add-on's deployment ID.

The deployment ID is an arbitrary string that helps the add-on developer identify the deployment containing the add-on manifest. Deployment IDs are required and can have at most 100 characters.

3. Click **Next**.

A side panel opens for you to submit the specification of the add-on manifest in JSON format. This is also called DEPLOYMENT.JSON.

The [add-on manifest file](/apps-script/add-ons/concepts/workspace-manifests) is the central configuration for a Google Meet add-on. The following code sample shows the available Meet fields for web in the add-on manifest file.

```json
{
  "addOns": {
    "common": {
      "name": "NAME",
      "logoUrl": "LOGO_URL"
    },
    "meet": {
      "web": {
        "sidePanelUrl": "SIDE_PANEL_URL",
        "supportsScreenSharing": SUPPORTS_SCREENSHARING,
        "addOnOrigins": ["ADD_ON_ORIGINS"],
        "logoUrl": "MEET_WEB_LOGO_URL",
        "darkModeLogoUrl": "DARK_MODE_LOGO_URL"
      }
    }
  }
}
```

Replace the following:

- **NAME**: String. The name of your Google Meet add-on.
- **LOGO_URL**: String. The URL of the logo for the Google Workspace add-on. This is used for the add-on across Google Workspace products.
- **SIDE_PANEL_URL**: String. The URL to the entry point of your add-on app. This is displayed in an iframe within the [side panel](/workspace/meet/add-ons/guides/overview#side-panel). The [origin](/workspace/meet/add-ons/guides/overview#origin) of this URL must be part of the origins specified in the ADD_ON_ORIGINS field.
- **SUPPORTS_SCREENSHARING**: Optional. Boolean. If set to false, users must use the add-on to see what's happening in a collaborative add-on session. If set to true, the initiator of the collaborative add-on session can screen share their view of the add-on.
- **ADD_ON_ORIGINS**: List of strings. A list of [origins](/workspace/meet/add-ons/guides/overview#origin) where your add-on is hosted. Two URLs have the same origin when they share the same scheme, host, and port. Sub origins are also permitted, as are wildcard subdomains. For more information, see [Add-on security](/workspace/meet/add-ons/guides/add-on-security).
- **MEET_WEB_LOGO_URL**: Optional. String. A Meet-specific URL of the logo for the add-on. This logo is used throughout Meet. If not present, the `logoUrl` from the common section is used. For logo design guidelines, see [Best practices](/workspace/meet/add-ons/guides/best-practices#logo-design).
- **DARK_MODE_LOGO_URL**: String. A dark mode specific URL of the logo for the add-on. Supplying a dark mode logo makes sure your add-on will look best in any Meet theme. For logo design guidelines, see [Best practices](/workspace/meet/add-ons/guides/best-practices#logo-design).

4. Click **Submit**.

For more information on deployments, see [Create a deployment resource](/workspace/add-ons/guides/alternate-runtimes#create_a_deployment_resource).

5. In the **App configuration** tab, under **App integration**, select **Google Workspace add-on**. Select **Deploy using cloud deployment resource** and then choose the correct HTTP deployment.

### Google Apps Script

1. Click the **App configuration** tab.

2. Under **App integration**, select **Google Workspace add-on**. Select **Deploy using Google Apps Script deployment ID** and enter your script's deployment ID.

3. Click **Save**.

For details on how to create an Apps Script project, see [Apps Script documentation](/apps-script/overview). The Meet add-on relies solely on the appsscript.json manifest file, also called the [Apps Script project manifest](/apps-script/concepts/manifests). Make sure the manifest file in your Apps Script project contains an `addOns` and a `meet` section.

The following code sample shows the available Meet fields in the add-on manifest file.

```json
{
  "addOns": {
    "common": {
      "name": "NAME",
      "logoUrl": "LOGO_URL"
    },
    "meet": {
      "web": {
        "sidePanelUrl": "SIDE_PANEL_URL",
        "supportsScreenSharing": SUPPORTS_SCREENSHARING,
        "addOnOrigins": ["ADD_ON_ORIGINS"],
        "logoUrl": "MEET_WEB_LOGO_URL",
        "darkModeLogoUrl": "DARK_MODE_LOGO_URL"
      }
    }
  }
}
```

Replace the following:

- **NAME**: String. The name of your Google Meet add-on.
- **LOGO_URL**: String. The URL of the logo for the Google Workspace add-on. This is used for the add-on across Google Workspace products.
- **SIDE_PANEL_URL**: String. The URL to the entry point of your add-on app. This is displayed in an iframe within the [side panel](/workspace/meet/add-ons/guides/overview#side-panel). The [origin](/workspace/meet/add-ons/guides/overview#origin) of this URL must be part of the origins specified in the ADD_ON_ORIGINS field.
- **SUPPORTS_SCREENSHARING**: Optional. Boolean. If set to false, users must use the add-on to see what's happening in a collaborative add-on session. If set to true, the initiator of the collaborative add-on session can screen share their view of the add-on.
- **ADD_ON_ORIGINS**: List of strings. A list of [origins](/workspace/meet/add-ons/guides/overview#origin) where your add-on is hosted. Two URLs have the same origin when they share the same scheme, host, and port. Sub origins are also permitted, as are wildcard subdomains. For more information, see [Add-on security](/workspace/meet/add-ons/guides/add-on-security).
- **MEET_WEB_LOGO_URL**: Optional. String. A Meet-specific URL of the logo for the add-on. This logo is used throughout Meet. If not present, the `logoUrl` from the common section is used. For logo design guidelines, see [Best practices](/workspace/meet/add-ons/guides/best-practices#logo-design).
- **DARK_MODE_LOGO_URL**: String. A dark mode specific URL of the logo for the add-on. Supplying a dark mode logo makes sure your add-on will look best in any Meet theme. For logo design guidelines, see [Best practices](/workspace/meet/add-ons/guides/best-practices#logo-design).

**Important:** Unlike other Google Workspace add-ons, Meet add-ons cannot be built entirely in Apps Script. You must, instead, build a full web app by [creating a side panel and main stage](/workspace/meet/add-ons/guides/quickstart). The side panel URL of your web app then must be specified under the SIDE_PANEL_URL of the appsscript.json manifest file.

## Install and test the add-on in Meet

To test your add-on in Meet, you must first install it for the signed-in user:

### HTTP deployment

1. Navigate to the Google Workspace Marketplace SDK for your project in Google Cloud console.
2. Click the **HTTP deployments** tab.
3. Click **Install** under the **Actions** column.

### Google Apps Script

1. Follow the Google Workspace add-on documentation to [Install an unpublished add-on](/workspace/add-ons/how-tos/testing-workspace-addons#install_an_unpublished).

You should now be able to use your add-on in a meeting. To try it, start a meeting at [meet.google.com](https://meet.google.com). The installed add-on is now visible in the Activities panel.

In addition to installing your add-on for the individual signed-in user, you can also [publish it](/workspace/meet/add-ons/guides/publish). When you publish your Google Workspace add-on, you make it available for others to find, install, and use.
