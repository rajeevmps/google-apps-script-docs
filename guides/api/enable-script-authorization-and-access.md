# Enable script authorization and access

## Page Summary

- Different types of authorizations are needed for the Apps Script API depending on whether you are using the API in your app or allowing other applications to manage your script project data.
- To use the Apps Script API within your application, you must enable the API in your application's Google Cloud project to create OAuth credentials.
- Granting third-party applications access to your script projects allows them to manage your script content and deployments, which carries some risk and requires explicit permission.
- Granting the Apps Script API access to your script projects is done through the Apps Script dashboard and applies to all applications, though individual applications still require authorization.

## Overview

The Google Apps Script API requires different types of authorizations depending on your goal:

- Use the Apps Script API in your app.
- Allow other applications to manage your script project data or deployments.

To use the Apps Script API in your application, you must enable the API in the application's [Google Cloud project](https://cloud.google.com/apis/docs/enable-disable-apis#enable_an_api). This lets you create OAuth credentials so that users of the application can authorize it.

To let third-party applications manage the content or deployment of your script projects, you must grant access to your script projects.

## Use the Apps Script API in your app

To use the Apps Script API inside your app, you must enable the Apps Script API in your application's Google Cloud project. After enabling the Apps Script API, you can create OAuth credentials and download the client ID and secret to include in your application. You can also monitor the API usage in the [Google Cloud console](https://console.cloud.google.com/).

You can use [the API enablement wizard](https://console.developers.google.com/start/api?id=script) to create or select a Google Cloud project in the Google Cloud console and automatically enable the API. Alternatively, you can [open the console's **Manage Resources** page](https://console.cloud.google.com/cloud-resource-manager), select a project, then search for and add the Apps Script API manually using the project's **APIs & services** dashboard. After you've enabled the API, you can create OAuth credentials, client IDs, and client secrets for your applications in the **APIs & services > Credentials** panel.

The [Apps Script API quickstarts](https://developers.google.com/apps-script/api/quickstart/python#step_1_turn_on_the_api_name) provide a step-by-step look at the whole process of enabling the API and setting up authorization for an application.

## Grant third-party applications access to your script projects

The Apps Script API can allow applications to create and modify your scripts and their [deployments](https://developers.google.com/apps-script/concepts/deployments). This can lead to a bad situation if you authorize a malicious third-party application which then proceeds to create more malicious scripts or modify the behavior of scripts you already have.

To help reduce this risk, the Apps Script API cannot access your script projects by default. You must explicitly grant the API access before you can use any application that creates or modifies scripts or deployments. Once you've granted the API access to your scripts, applications you authorize can use the API to manage your script projects.

An error results if you attempt to run an affected application without first granting the API access. This error occurs after you authorize the application.

**Note:** Applications can use the Apps Script API to [execute Google Apps Script functions](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run). These API requests don't require granting access to your script projects.

You can grant the Apps Script API access to your script projects using the [Apps Script dashboard](https://developers.google.com/apps-script/guides/dashboard#settings). You can also use the dashboard to revoke this access at any time. When you grant the API access, you are doing so for all applications. Individual applications still need to be authorized, however.

Before you grant access, ensure you understand the risk involved in allowing applications to modify your scripts. Never authorize any application that you suspect is malicious.

Source: https://developers.google.com/apps-script/api/how-tos/enable
