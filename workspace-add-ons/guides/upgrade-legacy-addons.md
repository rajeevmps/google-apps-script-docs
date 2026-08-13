# Upgrade legacy Gmail and Calendar add-ons

You can't directly upgrade Editor add-ons into Google Workspace add-ons. For more information, see Can I upgrade my Editor add-on.

If you've already published an add-on for Gmail or Calendar, you can upgrade it to a Google Workspace add-on. This page describes how to add Google Workspace functionality to your add-on and publish it.

Transfer the new functionality to your original add-on to retain the Google Workspace Marketplace listing, installs, and users. Upgrading also lets you use features like homepages.

If you don't upgrade your Gmail and Calendar add-ons, the application automatically upgrades them to add-ons with a generic homepage. No change to your listing or code is required. The add-on remains available only in its host application. The Google Workspace Marketplace lists auto-upgraded add-ons in the "works with Gmail" or "works with Calendar" sections. It retains the listing, installs, and users.

## 1. Copy the Apps Script project

The upgraded add-on uses the same Google Cloud project as your published add-on, but create a copy of the script project first so that you don't affect existing users during testing. Upgrading a copy also ensures you have the original code and can redeploy it if necessary.

1.  Open the existing script project.
2.  Select **Overview** info_outline.
3.  Select **Make a copy** content_copy.
4.  Select **Project Settings > Change project**.
5.  Select **GCP Project Number**.
6.  Enter the project number associated with your published add-on.
7.  Select **Set project**.

**Warning:** Don't upgrade a public project directly. Use a copy to keep the upgraded version separate from the public version during construction and testing.

## 2. Integrate Google Workspace add-on

Implement the add-on features.

1.  Plan what content to show in homepage cards. If you want homepages for multiple hosts, decide whether they can share content or need custom cards.
2.  In the copied script project, build homepage cards with `homepageTrigger` functions.
3.  Consider adding contextual cards, like for extending the Gmail interface or extending the Calendar interface.

    **Caution:** Upgraded add-ons receive a different ID for Gmail messages than legacy add-ons. This only affects add-ons that use `messageId` as a key in permanent storage. To get old ID values, use the Gmail API. The `messages.get` method accepts both ID formats but returns the old format.

4.  Update any code that accesses event objects to use the new structure. The new structure contains the same fields, but the original ones are deprecated.

## 3. Update the manifest

The manifest structure for Google Workspace add-ons is significantly different from legacy add-ons. Update the project's manifest fields using the following tables. Move all relevant subproperties to the `addOns` property.

Update the `oauthScopes` field to reflect the permissions the updated add-on requires.

See Manifests.

### Gmail add-ons

| Original manifest field | Action required |
|---|---|
| `gmail.composeTrigger` | Move to `addOns.gmail.composeTrigger`. |
| `gmail.contextualTriggers[]` | Move the list to `addOns.gmail.contextualTriggers[]`. |
| `gmail.logoUrl` | Move to `addOns.common.logoUrl`. |
| `gmail.name` | Move to `addOns.common.name`. |
| `gmail.openLinkUrlPrefixes[]` | Move the list to `addOns.common.openLinkUrlPrefixes[]`. |
| `gmail.primaryColor` | Move to `addOns.common.layoutProperties.primaryColor`. |
| `gmail.secondaryColor` | Move to `addOns.common.layoutProperties.secondaryColor`. |
| `gmail.universalActions[]` | Move the list to `addOns.common.universalActions[]`. |
| `gmail.universalActions[].text` | Move each `gmail.universalActions[].text` field to a corresponding `addOns.common.universalActions[].label` field. |
| `gmail.useLocalFromApp` | Move to `addOns.common.useLocaleFromApp`. |

### Calendar conferencing add-ons

| Original manifest field | Action required |
|---|---|
| `calendar.createSettingsUrlFunction` | Move to `addOns.calendar.createSettingsUrlFunction`. |
| `calendar.conferenceSolution[]` | Move to `addOns.calendar.conferenceSolution[]`. |
| `calendar.logoUrl` | Move to `addOns.common.logoUrl`. |
| `calendar.name` | Move to `addOns.common.name`. |

## 4. Test the upgraded add-on

To test your upgraded add-on, you need to install it as an unpublished add-on.

1.  Open the script project in the Apps Script editor.
2.  Select **Deploy > Test deployments**.
3.  Select **Install**.
4.  At the bottom, select **Done**.

After you install the add-on, it's immediately available in the host applications it extends. You might need to refresh the host application tab before the add-on appears.

When testing, make sure to:

*   Test card navigation flows in all host applications.
*   Use example test data.
*   If your add-on connects to a third-party API, verify that authorization and sign-in work correctly.
*   Handle error conditions gracefully.

For more details, see Test and debug Apps Script Google Workspace add-ons.

## 5. Request reviews

Approval is required for all add-ons before they're listed in the Google Workspace Marketplace.

To submit for review, follow these steps:

1.  Fulfill the publishing requirements.
2.  Create a versioned deployment using the code to publish. Don't publish using a head deployment.
3.  If you added scopes, request OAuth verification. Submit them for verification as early as possible. Verify the add-on before you proceed.

## 6. Make the add-on available

1.  Open the Google Workspace Marketplace SDK.
2.  Select **Configuration**.
3.  Update the description and screenshots.
4.  Under **Extensions**, select **Upgrade to Google Workspace add-on**. In the box, enter the **deployment ID**.

    **Caution:** This is a one-time process and can't be undone.

5.  If you added scopes, add them to the **OAuth 2.0 scopes** section. They must exactly match the manifest.
6.  Verify the information and select **Save changes**.

If you have questions, contact support.

## FAQ

Answers to frequently asked questions about add-on upgrades.

### Can I upgrade my Editor add-on?

Most Editor add-ons can move over to Google Workspace add-ons. However, the upgrade process is more complex than for legacy add-ons.

To migrate an Editor add-on, rewrite the UI as a card-based interface and use the Card Service.

Some services might not be available. For example, there's no file picker in the Card Service.

### Can I build a separate Google Workspace add-on and keep my existing one?

You can build add-ons under different brand names, but we don't permit separate add-ons under the same brand name as your Google Workspace add-on. If you want to request an exception, contact support.

### Will users need to re-authorize the add-on?

As long as the add-on uses the same Cloud project, users don't need to reauthorize previously approved permissions. However, if you add scopes, they must authorize them.

### Can I upgrade a Chrome extension and transfer users?

No. You can't transfer a Chrome extension's users, installs, or reviews. Create a new Google Workspace add-on and direct users to the Google Workspace Marketplace.

### Can I bundle add-ons?

See List app integrations Together.
