# OAuth Client Verification

Apps Script projects that request sensitive OAuth scopes.

**Google OAuth clients that request certain sensitive OAuth scopes are
subject to verification by Google.** For a high-level overview of the
authorization process, see
[Authorization for Google Services](https://developers.google.com/apps-script/guides/services/authorization).

Verification isn't required for Google Apps Script projects
whose owner and users belong to the same Google Workspace domain or customer.

If you don't verify your script project's OAuth client, users outside your
domain see an unverified app screen when they try to authorize your script.
An unverified authorization flow allows these users to authorize unverified
apps and use them, but only after confirming they understand the risks. The
total number of unverified app users is also capped.

For more information, see the following articles:

- [Unverified Apps](https://support.google.com/cloud/answer/7454865)
- [OAuth Application Verification FAQ](https://support.google.com/cloud/answer/9110914)
- [Google API Services: User Data Policy](https://developers.google.com/terms/api-services-user-data-policy)

![The unverified app warning screen.](https://developers.google.com/static/apps-script/images/unverified2.png) **Figure 1**: Unverified app screen ![An animated GIF showing the authorization flow for an unverified app.](https://developers.google.com/static/apps-script/images/unverified-app-ui.gif) **Figure 2**: Unverified app authorization flow

This change applies to Google OAuth web clients, including those used by all
Apps Script projects. By
[verifying your app with Google](https://developers.google.com/apps-script/guides/client-verification#request_verification),
you can remove the unverified app screen from your authorization flow and
give your users confidence that your app is non-malicious.

## Unverified apps

Google Workspace add-ons, web apps, and other deployments (such as apps that use the
[Apps Script API](https://developers.google.com/apps-script/api)) may need verification.

add-ons are no longer verified as part of the
[Google Workspace add-on review process](https://developers.google.com/workspace/add-ons/concepts/gmail-addon-review), and
must be verified prior to publishing an add-on.

### Applicability

If the app uses sensitive OAuth scopes, the unverified app screen may appear
as part of the authorization flow. Its presence (and the resulting unverified
app authorization flow) depends on what account the app is published from and
what account is attempting to use the app. For example, apps published
internally within a specific Google Workspace organization don't result in the
unverified app authorization flow for accounts in that domain, even if the app
hasn't been verified.

The following table illustrates what situations result in the unverified app
authorization flow:

|   | Client is verified | Publisher is a Google Workspace account of customer A | Script is in a shared drive of customer A | Publisher is a Gmail account |
|---|---|---|---|---|
| User is a Google Workspace account of customer A | Normal auth flow | Normal auth flow | Normal auth flow | ***Unverified auth flow*** |
| User is a Google Workspace account **not** of customer A | Normal auth flow | ***Unverified auth flow*** | ***Unverified auth flow*** | ***Unverified auth flow*** |
| User is a Gmail account[**^1^**](https://developers.google.com/apps-script/guides/client-verification#note1) | Normal auth flow | ***Unverified auth flow*** | ***Unverified auth flow*** | ***Unverified auth flow*** |

**^1^**Any Gmail account, including the account used to
publish the app.

### User cap

The number of users who can authorize an app using the unverified app flow is
capped to limit possible abuse. See
[OAuth application user limits](https://support.google.com/cloud/answer/9028764)
for details.

## Request verification

You can request verification of the OAuth client used by your app and its
associated Google Cloud project. Once your app is verified, your users no
longer see the unverified app screen. In addition, your app is no longer
subject to the [user cap](https://developers.google.com/apps-script/guides/client-verification#user_cap).

### Requirements

In order to submit your OAuth client for verification, you must satisfy the
following requirements:

1. You must own a website on a domain. The site must host publicly-accessible
   pages that describe your app and its privacy policy. You must also
   [verify your ownership of the site with Google](https://support.google.com/webmasters/answer/9008080?ref_topic=7440006).

   You don't need to publish your app from an account in this
   domain, but the domain owner must be an editor or owner of the script
   project.
2. The [Google Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects)
   your script project uses must be a
   [standard Google Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#standard_cloud_platform_projects)
   that you have edit access for. If your script is using its default
   Google Cloud project, you must
   [switch to a standard Google Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#use_a_different_standard_project).

In addition, you must have the following **required** assets:

- **Application name** . The name of the app; this is displayed on the consent screen. It should match the name used for the app in other locations, such as the [Google Workspace Marketplace](https://developers.google.com/workspace/marketplace) listing for published apps.
- **Application logo**. A app logo JPEG, PNG, or BMP image to use in the consent screen. Its file size must be 1MB or less.
- **Support email**. This is an email displayed on the consent screen for users to contact if they need app support. It can be your email address or a Google Group that you own or manage.
- **Scopes** . The list of all the [scopes](https://developers.google.com/apps-script/concepts/scopes) your app uses. You can [view your scopes](https://developers.google.com/apps-script/concepts/scopes#viewing_scopes) in the Apps Script editor.
- **Authorized domains**. This is a list of domains containing information about your app. All your application's links (such as its required privacy policy page) must be hosted on authorized domains.
- **Application homepage URL**. The location of a homepage describing your app. This location must hosted on an authorized domain.
- **Application privacy policy URL**. The location of a page describing your app's privacy policy. This location must be hosted on an authorized domain.

In addition to the preceding required assets, you can optionally provide an
**Application terms of service URL** that points to a page describing your
app's terms of service. If provided, this location must be in an authorized
domain.

### Steps

1. If you have not done so already, [verify ownership of all the authorized domains](https://support.google.com/webmasters/answer/9008080?ref_topic=7440006) you use to host your script project's privacy policy and other information. The verified owners of the domains must be editors or the owner of the script project.
2. In the Apps Script project, click **Overview** . Under **Project OAuth Scopes**, copy the scopes that your script project uses.
3. [Complete the OAuth consent screen for your application's
   Google Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#completing_the_oauth_consent_screen)
   using the text and URL assets you collected.

   1. List the **Authorized domains** where your app's information (such as its privacy policy) are hosted.
   2. To add your application scopes, click **Add or Remove Scopes** . The
      resulting dialog attempts to autodetect scopes for APIs you've enabled
      in the Google Cloud console (such as
      [advanced services](https://developers.google.com/apps-script/guides/services/advanced)). You can
      select scopes from this list by checking the corresponding boxes.

      This autodetected list doesn't always include scopes used by
      Apps Script [built-in services](https://developers.google.com/apps-script/guides/services).
      You must enter these scopes under **Manually add scopes**.

      When you're done, click **Update**.
4. When you've entered all the required information, click **Save**.

5. Click **Submit for verification** to start a verification request.

Most verification requests receive a response within 24 to 72 hours.
You can check the **Verification status** at the top of the OAuth consent
screen form. When verification of your OAuth client is confirmed, your app is
verified.

If your app is verified and later you decide to
[switch to another Google Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#use_a_different_standard_project),
you must repeat these steps to keep the app verified.